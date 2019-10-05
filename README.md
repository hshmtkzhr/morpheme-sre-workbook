# Morphological Analysis for SRE Workbook

## install tree-tagger
```bash
mkdir ~/tree-tagger
cp tree-tagger-macos/* ~/tree-tagger
cd ~/tree-tagger
sh install-tagger.sh
echo 'PATH=$PATH: ~/tree-tagger/cmd:~/tree-tagger/bin' >> ~/.bash_profile
source ~/.bash_profile
```

## analyze
```bash
cd intermidiate-outputs
cat ../the-site-reliability-workbook-next18.txt | tree-tagger-english | tr [:upper:] [:lower:] > analyzed.txt
cat analyzed.txt | awk '$2 ~ /^jj|^nn|^r|^v/ {print $0}' > main-parts-of-speech.txt
cat main-parts-of-speech.txt  | awk '{print $1,$2}' | sort | uniq -c | sort -rn > parts-rank.txt
cat analyzed.txt | awk '$2 ~ /^np/' | sort | uniq -c | sort -rn > proper-noun.txt
```
