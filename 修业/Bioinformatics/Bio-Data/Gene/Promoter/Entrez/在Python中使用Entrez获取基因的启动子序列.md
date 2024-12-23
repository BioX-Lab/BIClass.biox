# 在Python中使用Entrez获取基因的启动子序列

本文通过Biopython中`Bio.Entrez`模块，演示访问Entrez获取相关基因（已知`Entrez Gene ID`）的启动子序列。
## 示例代码

``` python
from Bio import Entrez, SeqIO


# 设置个人电子邮件地址

Entrez.email = "your_email@example.com"
  

def fetch_gene_record(gene_id):

    """

    使用 Entrez.efetch 获取指定基因ID的XML记录。

  

    参数:

    gene_id (str): 基因的Entrez ID。

  

    返回:

    dict: 包含基因信息的字典，或 None 如果发生错误。

    """

    try:

        with Entrez.efetch(db="gene", id=gene_id, retmode="xml") as handle:

            gene_record = Entrez.read(handle)

        return gene_record

    except Exception as e:

        print(f"Error fetching gene record for ID {gene_id}: {e}")

        return None

  

def parse_gene_location(gene_record):

    """

    解析基因记录以获取基因的访问号、起始位置、结束位置和链方向。

  

    参数:

    gene_record (dict): 包含基因信息的字典。

  

    返回:

    tuple: 包含基因访问号、起始位置、结束位置和链方向的元组，或 None 如果解析失败。

    """

    try:

        gene_locus = gene_record[0]['Entrezgene_locus'][0]

        gene_accession = gene_locus['Gene-commentary_accession'] + '.' + gene_locus['Gene-commentary_version']

        gene_start = gene_locus['Gene-commentary_seqs'][0]['Seq-loc_int']['Seq-interval']['Seq-interval_from']

        gene_end = gene_locus['Gene-commentary_seqs'][0]['Seq-loc_int']['Seq-interval']['Seq-interval_to']

        gene_strand = gene_locus['Gene-commentary_seqs'][0]['Seq-loc_int']['Seq-interval']['Seq-interval_strand']['Na-strand'].attributes.get('value')

        return gene_accession, gene_start, gene_end, gene_strand

    except Exception as e:

        print(f"Error parsing gene location: {e}")

        return None

  

def calculate_upstream_coordinates(gene_start, gene_end, gene_strand, upstream_bp=500):

    """

    计算上游序列的起始和结束位置。

  

    参数:

    gene_start (int): 基因的起始位置。

    gene_end (int): 基因的结束位置。

    gene_strand (str): 基因链的方向，'plus' 或 'minus'。

    upstream_bp (int): 上游序列的长度（默认为500bp）。

  

    返回:

    tuple: 包含上游序列起始和结束位置的元组。

    """

    if gene_strand == 'plus':

        upstream_start = int(gene_start)+1 - upstream_bp

        upstream_end = int(gene_start)

    elif gene_strand == 'minus':

        upstream_start = int(gene_end) + 1

        upstream_end = int(gene_end) + upstream_bp

    else:

        raise ValueError(f"Unknown strand direction: {gene_strand}")

    return upstream_start, upstream_end

  

def fetch_upstream_sequence(gene_accession, upstream_start, upstream_end, strand):

    """

    使用 Entrez.efetch 获取指定范围内的上游序列。

  

    参数:

    gene_accession (str): 核苷酸序列的访问号（例如，NM_000546）。

    upstream_start (int): 上游序列的起始位置。

    upstream_end (int): 上游序列的结束位置。

    strand (str): 基因链的方向，'plus' 或 'minus'。

  

    返回:

    SeqRecord: 包含上游序列的 SeqRecord 对象，或 None 如果发生错误。

    """

    try:

        with Entrez.efetch(db="nucleotide", id=gene_accession, rettype="fasta", strand=strand, seq_start=upstream_start, seq_stop=upstream_end) as handle:

            upstream_seq_record = SeqIO.read(handle, "fasta")

        # 如果是负链，需要反转补基序

        if strand == 'minus':

            upstream_seq_record.seq = upstream_seq_record.seq.reverse_complement()

        return upstream_seq_record

    except Exception as e:

        print(f"Error fetching upstream sequence: {e}")

        return None

  

def get_upstream_sequence(gene_id, upstream_bp=500):

    """

    获取指定基因的上游序列。

  

    参数:

    gene_id (str): 基因的Entrez ID。

    upstream_bp (int): 上游序列的长度（默认为500bp）。

  

    返回:

    SeqRecord: 包含上游序列的 SeqRecord 对象，或 None 如果发生错误。

    """

    gene_record = fetch_gene_record(gene_id)

    if not gene_record:

        return None

  

    gene_info = parse_gene_location(gene_record)

    if not gene_info:

        return None

  

    gene_accession, gene_start, gene_end, gene_strand = gene_info

  

    print(f"Gene ID: {gene_id}, Accession: {gene_accession}, Start: {gene_start}, End: {gene_end}, Strand: {gene_strand}")

  

    upstream_start, upstream_end = calculate_upstream_coordinates(gene_start, gene_end, gene_strand, upstream_bp)

  

    print(f"Upstream Start: {upstream_start}, Upstream End: {upstream_end}")

  

    upstream_seq_record = fetch_upstream_sequence(gene_accession, upstream_start, upstream_end, gene_strand)

    return upstream_seq_record

  

# 替换为所需Entrez Gene ID

gene_id = '3605'

upstream_seq = get_upstream_sequence(gene_id)

  

if upstream_seq:

    print("Upstream sequence (500bp):")

    print(upstream_seq.seq)

else:

    print("Failed to retrieve the upstream sequence.")
```

## 写在后面
网络访问遇到问题较多，不适合高频次访问。

#Entrez #Promoter #Python