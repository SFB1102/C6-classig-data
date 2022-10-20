# CLASSIG Data

This repository contains the gold data sets, automatically created annotations, and evaluation results from my dissertation *"Computational Methods for Investigating Syntactic Change: Automatic Identification of Extraposition in Modern and Historical German"*.

All files in this repository are provided in the [CoNLL-U Plus format](#data-format), which can be readily processed with the [CLASSIG pipeline](https://github.com/rubcompling/classig-pipeline).

The repository includes all data sest that I am allowed to make publicly available. For data sets with restrictive licences (TüBa-D/Z, TüBa-D/S, Tiger), I include information on the train/dev/test splits to make my experiments and results more transparent. For access to the original data, please contact [me](mailto:ortmann@linguistics.rub.de).

Due to space constraints, the data sets and language models from the example analysis in the dissertation cannot be stored in this Git repository. Instead, all resources that can be shared publicly - including the data from this repository - are provided for download at [Zenodo](https://doi.org/10.5281/zenodo.7180973).

## Content of this Documentation

1. [Repository Structure](#repository-structure)  
    1.1. [Gold Data](#gold-data)  
    1.2. [System Annotations](#system-annotations)  
    1.3. [Evaluation Results](#evaluation-results)  
    1.4. [Additional Data](#additional-data)  
           1.4.1 [Example Annotations](#example-annotations)  
           1.4.2 [Language Models](#language-models)  
2. [Data Format](#data-format)  
3. [Annotation Format](#annotation-format)  
    3.1. [Antecedents](#antecedents)  
    3.2. [Chunks](#chunks)  
    3.3. [Extraposition Candidates](#extraposition-candidates)  
    3.4. [Phrases](#phrases)  
    3.5. [Topological Fields](#topological-fields)  
4. [License](#license)  
5. [References](#references)  


## Repository Structure

### Gold Data

The `gold` folder contains the data sets that were used as training and evaluation data for the annotation experiments in the thesis (topological field parsing, chunking, phrase and relative clause recognition, identification of RelC antecedents and extraposition). The different annotations are included in separate columns:

- `TOPF` : Topological field parsing
- `CHUNK` : Chunking
- `PHRASE` : Phrase recognition
- `Antec` : Antecedent identification
- `MovElem` : Extraposition identification (including RelC annotation)

The following table gives an overview of which annotations are available for which corpus:

| Corpus |  Topological fields | Chunks | Phrases | Relative clauses | Extraposition (and antecedents) | Reference               | License |
|:-------| ------------------- | ------ | ------- | ---------------- | ------------------------------- | ----------------------- | ------- |
TüBa-D/Z  |  :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark:  | Telljohann et al. 2017 | Restricted access |
Tiger  |  :x: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | (:heavy_check_mark: RelCs only)  | Brants et al. 2004 | Restricted access |
TüBa-D/S   |  :heavy_check_mark: | :x: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark:  | Hinrichs et al. 2000 | Restricted access |
Modern  |  :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark:  | Ortmann et al. 2019 | [CC BY-SA 3.0](https://creativecommons.org/licenses/by-sa/3.0/) and [CC BY–NC–ND 4.0](https://creativecommons.org/licenses/by-nc-nd/4.0/deed.de) |
Mercurius  | :x: | :heavy_check_mark: | :heavy_check_mark: | :x: | :x:  | Demske 2005 | [CC BY 3.0](https://creativecommons.org/licenses/by/3.0/) |
ReF.UP  | :x: | :heavy_check_mark: | :heavy_check_mark: | :x: | :x:  | Demske 2019, Wegera et al. 2021 | [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/) |
HIPKON  | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark:  | Coniglio et al. 2014 | [CC BY 3.0](https://creativecommons.org/licenses/by/3.0/)
DTA   |  :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark:  | BBAW 2019 | [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/) |

For corpora with restricted access, I specify the train/dev/test splits in the corpus folder (Tiger, TüBa-D/Z). The TüBa-D/S corpus was used only as test data.
Annotations for the other corpora are provided in a custom BIO format (see the documentation [below](#annotation-format)).

- - - - - - - - - - - - - - - - 

### System Annotations

The `system` folder contains the annotations that were created automatically with the different models (`Punct`, `News1`, `News2`, `Hist`, `Mix`) as described in the thesis.
They can be reproduced by applying the [CLASSIG pipeline](https://github.com/rubcompling/classig-pipeline) to the gold data sets.

Historical models (`Hist`, `Mix`) were only applied to historical data.

The files are ordered by :arrow_right_hook: Corpus :arrow_right_hook: Annotation :arrow_right_hook: Model and contain only the respective annotation of the respective model.

- - - - - - - - - - - - - - - - 

### Evaluation Results

The `eval` folder contains the evaluation results from the annotation studies and the results of the example analyses:

- The folders `antec`, `brackets`, `chunks`, `extrap`, `phrases`, `relc`, and `topf` include evaluation results for each system annotation with the different models (cf. above). The files contain traditional and fair evaluation results for individual files, labels, and overall.  
- The `orality` folder contains the results of the orality analysis with the [COAST implementation](https://github.com/rubcompling/COAST). The folder includes two files per data set from the example analysis: one with the raw feature values (`_results.csv`) and one with scaled results and the orality score for this specific data set (`_results_scaled.csv`). The folder also contains a file with raw feature values for all data sets (`all_results.csv`) and scaled feature values and orality scores across all data sets (`all_results_scaled.csv`).
- The `surprisal` folder includes results of the information-theoretic example analysis. For each RelC, the respective corpus, filename, sentence ID, RelC ID, position (insitu/ambig/extrap), length in words, mean unigram POS surprisal, mean unigram word surprisal, mean bigram POS surprisal, and mean bigram word surprisal is given.
- The results of the example analysis with DORM are included in the `dorm` folder. There is one file with DORM calculated from bigram surprisal on a word basis and one with DORM calculated from bigram surprisal on a constituent basis. For each sentence with extraposed relative clause and its variant sentence with in situ RelC, the respective corpus, filename, sentence ID, DORMorig, DORMvariant, and DORMdiff for POS surprisal and DORMorig, DORMvariant, and DORMdiff for word form surprisal are given.

The evaluation results can be reproduced with the [CLASSIG pipeline](https://github.com/rubcompling/classig-pipeline), the gold and system annotations (see above), and the data from the example analysis (provided at [Zenodo](https://doi.org/10.5281/zenodo.7180973)).

- - - - - - - - - - - - - - - - 

### Additional Data

The [downloadable data](https://doi.org/10.5281/zenodo.7180973) also includes the data sets and language models that were used for the example analysis. The intention of the analysis was to demonstrate the usefulness of automatic annotation methods for the analysis of *large* data sources. However, the size of the data samples (several hundred books, etc.) are beyond the storage limits of standard Git repositories. Instead, the data is freely available via [Zenodo](https://doi.org/10.5281/zenodo.7180973).

#### Example Annotations

The `example` folder (downloadable at [Zenodo](https://doi.org/10.5281/zenodo.7180973)) contains the annotated data for the example analysis (except data sets with restricted access: TüBa-D/S, TüBa-D/Z, Tiger, cf. above).
The following annotations are provided: 

- `TOPF` : Column with topological fields in [BIO format](#annotation-format) (see [Topological Fields](#topological-fields))
- `TopFString` : Topological field parse in bracket notation as sentence attribute (see [Topological Fields](#topological-fields))
- `PTBstring` : Constituency parse in bracket notation as sentence attribute (see [Phrases](#phrases))
- `Antec` : Antecedents of relative clauses in [BIO format](#annotation-format) (see [Antecedents](#antecedents))
- `MovElem` : Extraposition annotation in [BIO format](#annotation-format) (see [Extraposition Candidates](#extraposition-candidates))

The modern data sets were annotated with the `Punct` and `News1` models. The historical data sets were annotated with the `Punct` and `Mix` models (except ReF.RUB, which was annotated with the `Punct` and `Hist` models).

| Models            |  Data sets                                      |
|:------------------| :---------------------------------------------- |
| `Punct` + `News1` | Gutenberg, OPUS, SdeWaC, SermonOnline, TüBa-D/W |
| `Punct` + `Mix`   | Anselm, DTAscience, GerManC, KaJuK, RIDGES      |
| `Punct` + `Hist`  | ReF.RUB                                         |

- - - - - - - - - - - - - - - - 

#### Language Models

The `lm` folder (downloadable at [Zenodo](https://doi.org/10.5281/zenodo.7180973)) contains the language models (`lm/models`) and test data for the surprisal analysis (`lm/surprisal`).

There are different n-gram language models for nine freely available data sets. The language models are named after n-gram size and annotation, e.g., `1-gram_XPOS` for a unigram model based on POS tags. The files contain two tab-separated columns with n-gram and frequency. n-grams (first column) are separated with spaces for n > 1. #S and #E are used as padding elements.

The `lm/surprisal` folder contains test data for the surprisal analysis of all freely available data sets. For Tiger, TüBa-D/S, and TüBa-D/Z, the filenames and sentence IDs of the test sentences are given. For each original test sentence (`lm/surprisal/corpus/surprisal`) with extraposed relative clause, there is a variant sentence for the analysis with DORM (`lm/surprisal/corpus/surprisal_variants`).

The language models can be reproduced and used for analyses with the [CLASSIG pipeline](https://github.com/rubcompling/classig-pipeline).

## Data Format

The data sets are provided in the [CoNLL-U Plus format](https://universaldependencies.org/ext-format.html). The first line of each file (starting with `# global.columns = `) specifies the columns that are included.

Columns are separated by tabs and sentences by empty lines. For each sentence, meta information can be given at the beginning of a sentence, e.g., the sentence ID and the concatenated tokens. Meta lines are preceded by the hash sign `#`.

Tokens are indexed starting at index 1. Empty annotations are indicated by an underscore `_`.

The following example shows the head of `opensubtitles.conllup` from the Modern data sample.

```
# global.columns = ID FORM LEMMA UPOS XPOS FEATS HEAD DEPREL DEPS MISC Antec CHUNK MovElem PHRASE TOPF
# sent_id = 1
# sent_id(TSV) = 1
# text = Du willst alles wissen .
1  Du      du      _   PPER   number=sg|person=2|case=nom|gender=*    4  subj  _  _  _  B-NC  B-NP-insitu  B-NP  B-VF
2  willst  wollen  _   VMFIN  number=sg|person=2|mood=ind|tense=pres  4  aux   _  _  _  O     _            O     B-LK
3  alles   alle    _   PIS    number=sg|case=acc|gender=neut          4  obj   _  _  _  B-NC  B-NP-insitu  B-NP  B-MF
4  wissen  wissen  _   VVINF  _                                       _  _     _  _  _  O     _            O     B-RK
5  .       .       _   $.     _                                       _  _     _  _  _  O     _            O     O
```

## Annotation format

Span annotations are encoded with BIO tags. The first letter of the tag specifies the position inside/outside of the span:

Letter | Meaning
 :---: | :-------------------------
 B     | beginning of the span
 I     | inside of the span
 O     | outside of any span

`B` and `I` are supplemented with the span label, separated by a dash: `B-NP` or `I-NP`. Tokens outside of spans are labeled as `O`. For sparse annotations that only concern few tokens (e.g., antecedents), the `O` can be replaced by an underscore `_` to improve the readability of the file for a human user.

A span can include one or more other spans. In this case, annotations are ordered hierarchically from the longest span to the left to the shortest, most deeply embedded span to the right. Multiple spans are seperated by a pipe `|`, e.g., `I-NF|B-LK`. This allows to encode complex hierarchical structures with BIO tags (as long as they are continuous). The following example displays a toy constituency tree with BIO tags.

```
Das         This        B-S|B-NP
ist         is          I-S|B-VP
ein         a           I-S|I-VP|B-NP
einfacher   simple      I-S|I-VP|I-NP|B-AP
Satz        sentence    I-S|I-VP|I-NP
.           .           I-S
```

For more complex annotations, the BIO-tags can be extended with additional information, e.g., `B-RELC-extrap-1`. For details on the different annotations, cf. the sections below.

1. [Antecedents](#antecedents)
2. [Chunks](#chunks)
3. [Extraposition candidates](#extraposition-candidates)
5. [Phrases](#phrases)
6. [Topological fields](#topological-fields)

- - - - - - - - - - - - - - - - 

### Antecedents

Antecedents are annotated in the `Antec` column. Antecedents can be nested, i.e., contain other antecedents. They usually have a head token, and they are always linked to a [candidate for extraposition](#extraposition-candidates) via an ID. The label consists of up to 4 parts, separated by dashes. Empty parts are ommited.

BIO letter | Antecedent | ID | Head |
:--------: | :---------- | :------ | :----- |
 B         |  Antec | 1, 2, ... | Head 
 I         |  Antec | -- | Head |
 
The beginning of an antecedent could be: `B-Antec-1` or `B-Antec-2-Head`  
A token inside of an antecedent could be annotated with: `I-Antec` or `I-Antec-Head`.

Additional remarks:
- `Head` is only annotated for the head token of the antecedent.
- `IDs` are unique within a given sentence, starting at index 1. They always refer unambiguously to a [candidate for extraposition](#extraposition-candidates) in the same sentence.
- If the same token span serves as antecedent for multiple extraposition candidates, this is annotated as if there were two distinct antecedents, e.g. `B-Antec-1|B-Antec-2`.
- Tokens that are not part of an antecedent are labeled with `_`.

- - - - - - - - - - - - - - - - 

### Chunks

Chunks are non-recursive, non-overlapping constituents from a sentence's parse tree. Chunk annotations are included in the `CHUNK` column. The following chunk labels are used:

Label | Chunk 
:---: | :----
NC | Noun chunk
PC | Prepositional chunk
AC | Adjective chunk
ADVC | Adverb chunk
sNC | Stranded noun chunk
sPC | Stranded prepositional chunk

Stranded chunks occur when the beginning of a chunk is separated from the rest of the chunk by pre-modifying elements. For more information, cf. [Ortmann (2021)](https://aclanthology.org/2021.nodalida-main.19/).

- - - - - - - - - - - - - - - - 

### Extraposition Candidates

Extraposition candidates are phrases/clauses that are or can be extraposed, i.e., moved to the post-field of the sentence. They are annotated in the `MovElem` column. The following types are considered in the dissertation:

Label | Element | 
:---: | :------ |
NP  | noun phrase |
PP  | prepositional phrase | 
AP  | adjective phrase | 
ADVP | adverb phrase | 
RELC | relative clause | 

Candidates can contain other constituents, e.g., a relative clause with embedded noun phrases.

The label of a candidate can consist of up to 4 parts, separated by dashes. Empty parts are ommited.

1. The first part specifies, whether the token is at the beginning `B` or inside `I` of the constituent.
2. The second part gives the type of constituent, e.g., `NP` or `RELC`.
3. The third part is only present for the beginning of constituents and specifies the position `extrap`, `insitu`, or `ambig`.
4. The fourth part specifies the ID, if the element has an [antecedent](#antecedents). It is only annotated for the first token of a constituent.

BIO letter | Element type | Position | ID |
:--------: | :---------- | :------ | :--- |
 B         |  NP, PP, AP, ADVP, RELC | extrap, insitu, ambig | 1, 2, ...
 I         |  NP, PP, AP, ADVP, RELC | -- | --

Exemplary labels for the beginning of a constituent could be: `B-NP-insitu`, `B-RELC-ambig-1`  
Labels inside of constituents could be: `I-AP`, `I-RELC`

Additional remarks:
- `IDs` are unique within a given sentence, starting at index 1. Only elements with an [antecedent](#antecedents) get an `ID`.
- Tokens outside of extraposition candidates are labeled with `_`.

- - - - - - - - - - - - - - - - 

### Phrases

In the context of this project, phrases are understood as non-overlapping constituents from a sentence's parse tree. They are annotated in the `PHRASE` column. Only the highest non-terminal nodes of the following types are included:

Label | Phrase 
:---: | :----
NP | Noun phrase
PP | Prepositional phrase
AP | Adjective phrase
ADVP | Adverb phrase

Phrases are expected to not cross topological field boundaries. This means that they can be located within a field or contain one or more fields. But the may not be part of two neighbouring fields, and the fields they contain may not stretch across the boundaries of the phrase. For more information, cf. [Ortmann (2021b)](https://konvens2021.phil.hhu.de/wp-content/uploads/2021/09/2021.KONVENS-1.11.pdf).

In pre-annotated data sets (Mercurius, ReF.UP, Tiger, TüBa-D/S, TüBa-D/Z), phrases were derived from the provided constituency trees. The `gold` folder contains the (linearized) original constituency trees (including grammatical functions) as `PTBstring` sentence attribute in standard bracket notation. The simplified trees that were used in the thesis are included in the `PTBstring_simple` attribute.

The system annotations (`system` folder) and the data sets from the example analysis include the automatically generated constituency trees as sentence attribute `PTBstring` (which corresponds to `PTBstring_simple` in the gold data), e.g.:

```
# PTBstring = (VROOT(SIMPX(VF(NX(PPER Ich)))(LK(VXFIN(VAFIN habe)))(MF(PX(APPR in)(NX:HD(PPOSAT Ihrem)(NN Keller)))(ADJX(ADJD zufällig))(NX(PIS etwas)))(VC(VXINF(VVPP gefunden)))(KOMMA ,)(NF(R(C(NX(PRELS was)))(MF(NX(PPER mich))(ADJX(ADJD wirklich)))(VC(VXFIN(VVFIN beunruhigt))))))(PUNKT .)) 
```

Annotations with the `News1` model follow the TüBa-D/Z annotation scheme (Telljohann et al. 2017). Annotations with the `News2`, `Hist`, and `Mix` models follow the Tiger annotation scheme (TIGER Project 2003). For more information on the models, consider the information in the thesis and the [CLASSIG pipeline documentation](https://github.com/rubcompling/classig-pipeline).

- - - - - - - - - - - - - - - - 

### Topological Fields

The topological field annotation is included in the `TOPF` column. Fields can be nested, i.e., one field can include one or more (possibly complex) other fields. The following field labels are used:

Label | Field 
:---: | :----
KOORD | Koordinationsfeld (*coordination field*)
LV | Linksversetzung (*left dislocation*)
VF | Vorfeld (*pre-field*)
LK | Linke Satzklammer (*left sentence bracket*)
MF | Mittelfeld (*middle field*)
RK | Rechte Satzklammer (*right sentence bracket*)
NF | Nachfeld (*post-field*)

The annotations are derived from the annotation scheme of the TüBa-D/Z corpus (Telljohann et al., 2017). For more information, cf. [Ortmann (2020)](https://aclanthology.org/2020.latechclfl-1.2.pdf)

For the system annotations (`system` folder) and the data sets from the example analysis, the automatically generated topological field parse is also included as a sentence attribute in standard bracket notation, e.g.:

```
# TopFString = (S(VF(PPER Ich))(LK(VAFIN habe))(MF(APPR in)(PPOSAT Ihrem)(NN Keller)(ADJD zufällig)(PIS etwas))(VC(VVPP gefunden))(KOMMA ,)(NF(C(PRELS was))(MF(PPER mich)(ADJD wirklich))(VC(VVFIN beunruhigt)))(PUNKT .))
```

The parses use labels from Telljohann et al. (2017). In the example, `VC` corresponds to `RK` and `C` corresponds to `LK` (cf. [Ortmann 2020](https://aclanthology.org/2020.latechclfl-1.2.pdf)).

## License

To the best of my knowledge, all provided data sets are free for non-commercial/academic use. Licenses for individual data sets differ:

Corpus | License(s) 
:----- | :-------------- |
Modern  |  [CC BY-SA 3.0](https://creativecommons.org/licenses/by-sa/3.0/) and [CC BY–NC–ND 4.0](https://creativecommons.org/licenses/by-nc-nd/4.0/deed.de) |
Tiger  |  Academic |
TüBa-D/S   |  Academic |
TüBa-D/W   | [CC BY-SA 3.0](https://creativecommons.org/licenses/by-sa/3.0/) |
TüBa-D/Z  | Academic |
Anselm | [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/) |
DTA   |   [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/) |
GerManC | [CC BY-NC-SA 3.0 DE](https://creativecommons.org/licenses/by-nc-sa/3.0/de/)
HIPKON  | [CC BY 3.0](https://creativecommons.org/licenses/by/3.0/) |
KaJuK   | [CC BY 3.0](https://creativecommons.org/licenses/by/3.0/) |
Mercurius  |  [CC BY 3.0](https://creativecommons.org/licenses/by/3.0/) |
ReF  | [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/) |
RIDGES Herbology | [CC BY 3.0](https://creativecommons.org/licenses/by/3.0/) |

For the remaining data sets (Gutenberg, OPUS, SdeWaC, SermonOnline), no explicit licenses are mentioned, but attribution is expected. 

If you plan to use any of the provided data sets, models, or results in your work, please cite the original authors and my thesis. Also, I strongly encourage you to consult the descriptions in the thesis for more detailed background information on resource creation, training, and evaluation.

## References

BBAW. 2019. Deutsches Textarchiv. [Grundlage für ein Referenzkorpus der neuhochdeutschen Sprache.](http://www.deutschestextarchiv.de/) Berlin-Brandenburgische Akademie der Wissenschaften.  

Sabine Brants, Stefanie Dipper, Peter Eisenberg, Silvia Hansen-Schirra, Esther König, Wolfgang Lezius, Christian Rohrer, George Smith, and Hans Uszkoreit. 2004. [TIGER: Linguistic interpretation of a German Corpus.](https://doi.org/10.1007/s11168-004-7431-3) In *Research on language and computation 2.4*, pp. 597–620.  

Marco Coniglio, Karin Donhauser, and Eva Schlachter. 2014. [HIPKON: Historisches Predigtenkorpus zum Nachfeld (Version 1.0)](https://doi.org/10.34644/laudatio-dev-yiTKCnMB7CArCQ9CxLhJ).  

Ulrike Demske. 2005. [Mercurius-Baumbank (Version 1.1).](https://doi.org/10.34644/laudatio-dev-VyQiCnMB7CArCQ9CjF3O) Universität Potsdam. 

Ulrike Demske. 2019. [Referenzkorpus Frühneuhochdeutsch: Baumbank.UP.](https://doi.org/10.34644/laudatio-dev-s0ImHH8BwG-ADazlg9LW) Universität Potsdam.  

Erhard W. Hinrichs, Julia Bartels, Yasuhiro Kawata, Valia Kordoni, and Heike Telljohann. 2000. [The Tübingen Treebanks for Spoken German, English, and Japanese.](https://doi.org/10.1007/978-3-662-04230-4_40) In *Verbmobil: Foundations of Speech-to-Speech Translation.* Ed. by Wolfgang Wahlster. Berlin: Springer, pp. 550–574.  

Katrin Ortmann, Adam Roussel, and Stefanie Dipper. 2019. [Evaluating Off-the-Shelf NLP Tools for German.](https://corpora.linguistik.uni-erlangen.de/data/konvens/proceedings/papers/KONVENS2019_paper_55.pdf) In *Proceedings of the Conference on Natural Language Processing (KONVENS)*, Erlangen, Germany, pp. 212-222. [[Github]](https://github.com/rubcompling/konvens2019)  

Katrin Ortmann. 2020. [Automatic Topological Field Identification in (Historical) German Texts.](https://aclanthology.org/2020.latechclfl-1.2.pdf) In *Proceedings of the The 4th Joint SIGHUM Workshop on Computational Linguistics for Cultural Heritage, Social Sciences, Humanities and Literature (LaTeCH-CLfL)*, Barcelona, Spain (online), pp. 10-18. [[Github]](https://github.com/rubcompling/latech2020)  

Katrin Ortmann. 2021a. [Chunking Historical German.](https://aclanthology.org/2021.nodalida-main.19/) In *Proceedings of the 23rd Nordic Conference on Computational Linguistics (NoDaLiDa)*, Reykjavik, Iceland (online), pp. 190-199. [[Github]](https://github.com/rubcompling/nodalida2021)  

Katrin Ortmann. 2021b. [Automatic Phrase Recognition in Historical German.](https://aclanthology.org/2021.konvens-1.11.pdf) In *Proceedings of the Conference on Natural Language Processing (KONVENS)*, Düsseldorf, Germany. [[Github]](https://github.com/rubcompling/konvens2021)

Katrin Ortmann. 2022. [Fine-Grained Error Analysis and Fair Evaluation of Labeled Spans.](https://aclanthology.org/2022.lrec-1.150.pdf) In *Proceedings of the Language Resources and Evaluation Conference (LREC), Marseille, France, pages 1400–1407. [[Github]](https://github.com/rubcompling/FairEval)

Heike Telljohann, Erhard W. Hinrichs, Sandra Kübler, Heike Zinsmeister, and Kathrin Beck. 2017. [Stylebook for the Tübingen Treebank of Written German (TüBa-D/Z).](https://www.sfs.uni-tuebingen.de/resources/tuebadz-stylebook-1707.pdf) Seminar fur Sprachwissenschaft, Universität Tübingen, Germany.  

TIGER Project. 2003. [TIGER Annotationsschema.](https://www.ims.uni-stuttgart.de/documents/ressourcen/korpora/tiger-corpus/annotation/tiger_scheme-syntax.pdf) Universität des Saarlands, Universität Stuttgart, Universität Potsdam.  

Klaus-Peter Wegera, Hans-Joachim Solms, Ulrike Demske, and Stefanie Dipper (2021). [Referenzkorpus Frühneuhochdeutsch (1350 – 1650), Version 1.0](https://www.linguistics.ruhr-uni-bochum.de/ref/), ISLRN 918-968-828-554-7.  
