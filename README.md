This repository contains experiments on the validation of data retrieved from Wikidata. Specifically, the validation of the data represented by the skos:altLabel property, which is supposed to describe synonym and variants of a concept. The experiment performs a comparison of the  tokens of the concept with synonyms retrieved from ConceptNet, considered a more trustable resource, with the aim of checking whether it is indeed a synonymy relation or of other kind (hierarchical).

<p align="center">
<img src="https://github.com/pmchozas/relval/blob/master/static/relval.png" width="80%" />
</p>

## Execution process

Your desired execution flow can be described in the configuration file, i.e. `configuration.json` as follows:

```javascript
{
	"source_language": "english",
	"run_id": "6",
	"source_file_dir": "Input/6term.csv",
	"gold_concepts_dir": "gold_concepts.json",
	"retrieve_wikidata": false,
	"retrieve_ConceptNet": false,
	"analysis": false,
	"evaluate": true
}
```

You can modify the variables in the configuration according to your data. These variables refer to: 

- `source_language`: the language of the input terms (only one language is accepted)
- `run_id` is an ID that you can set for your execution. The resulting files will be named according to this variable
- `retrieve_wikidata` should be set to `true` to retrieve data from Wikidata. The output is saved in the `Wikidata` folder.
- `retrieve_ConceptNet` is set to `true` to retrieve synonyms of the alternative labels on ConceptNet. In this part of the program, the induction rules are also applied over the alternative labels and the original terms using the axioms described in the paper (four semantic relationships are taken into account: `synonymy`, `relatedness`, `hyponymy` and `hypernymy`. The output is saved in the `Induction` folder.
- `analysis` is set to `true` to run a statistical analysis on which parts of the information are retrieved. It also creates the output of the axioms in a file in the `output` folder. 
- `evaluate` evaluate the output of the approach with respect to the gold-standard file `goldstandard.json`. The results are saved in the `Evaluation` folder.

Please note that the `gold_concepts.json` file may vary depending on the terminological domain. 

The output of each part of the program is saved in a specific directory in JSON format. The final output is also provided in RDF. 

A successful execution of the program looks like the following: 

```
============ Reading the configuration file
====== Retrieving data from Wikidata:
discrimination
maternity leave
public policy
case law
Appellanten
claim
====== Retrieving data from ConceptNet:
diskriminierung
discrimination
discrimination
discriminación
discriminatie
mutterschaftsurlaub
zwangerschaps- en bevallingsverlof
public policy
public policy
public policy
políticas públicas
fallrecht
case law
jurisprudencia
jurisprudentie
appellanten
==== Saving induced data.
====== Analysing valid outputs
All translations 30
Empty items: 0
Empty A: 7
Empty S: 8
All valids: 15
====== Evaluating the performance
=== Saving evaluation results.
============ Finished.
```

## Citation
Martín-Chozas, P., Ahmadi, S., and Montiel-Ponsoda, E. (2020). Defying Wikidata: Validation of Terminological Relations in the Web of Data. In Proceedings of the 12th Language Resources and Evaluation Conference (LREC), 5654-5659.

