# Summary

The Czech-PDTC UD treebank is based on the Prague Dependency Treebank – Consolidated
(PDT-C) 2.0, created at the Charles University in Prague.


# Introduction

[PDT-C](https://ufal.mff.cuni.cz/pdt-c)
is a collection of four treebanks that were previously released independently
and that are now enhanced with further manual linguistic annotation:

* **PDT:** The original [Prague Dependency Treebank](https://ufal.mff.cuni.cz/pdt3.5),
  based on texts from daily newspapers, a business weekly, and a popular science magazine, all from 1990s.
* **PCEDT:** The Czech part of the [Prague Czech-English Dependency Treebank](https://ufal.mff.cuni.cz/pcedt2.0/).
  The texts are Czech translations of the Wall Street Journal data in the Penn Treebank.
* **PDTSC:** [Prague Dependency Treebank of Spoken Czech](https://ufal.mff.cuni.cz/pdtsc2.0).
  It contains transcriptions of spontaneous dialogs from the Malach and Companions projects.
* **Faust:** A small dataset prepared for the [Faust](https://ufal.mff.cuni.cz/grants/faust) project.
  It contains user-generated Czech translations of English sentences, created during testing a machine
  translation system.

The treebank consists of 3.4 M tokens. It is licensed under the terms of
[CC BY-NC-SA 4.0](http://creativecommons.org/licenses/by-nc-sa/4.0/)
and its original (non-UD) version can be downloaded from
[http://hdl.handle.net/11234/1-5813](http://hdl.handle.net/11234/1-5813).

The morphological and syntactic annotation of the Czech UD treebank is created
through a conversion of PDT-C data. The conversion procedure has been designed by
Daniel Zeman and implemented in Treex.


# Domains and Data Split

NOTE: While the official release package on Lindat has only one training file
(like other UD treebanks), in the GitHub repository the file is split to
smaller parts because of GitHub file size restrictions. The individual files
correspond to the sources of the original texts; even in the merged file
the sources may still be distinguished, if desirable, by the prefixes of
sentence ids (indicated in parentheses below).

* l (ln) and m (mf) are mainstream daily papers (news, commentaries, but also
  sports results and TV programs)
* c (cmpr) is a business weekly
* v (vesm) contains popular scientific articles (the hardest to parse: long
  sentences and unusual vocabulary)
* w (wsj) are the translated texts from the Wall Street Journal.
* s (pdtsc) are the transcribed dialogs from PDTSC.
* f (faust) are the segments from the Faust project.

The dev and test sets contain all sources and their size is proportional
to the sizes of the respective training parts.


## Source of annotations

This table summarizes the origins and checking of the various columns of the CoNLL-U data.
In the original PDT, manual annotation was done by two annotators and then an arbiter.
This does not hold for all parts of PDT-C; however, double annotation was performed randomly
at several places, and the whole dataset underwent numerous automatic quality checks.
Patterns revealed by automatic consistency tests were checked by human annotators again.
Additional consistency tests were performed after conversion to UD.

| Column | Status |
| ------ | ------ |
| ID     | Sentence segmentation and (surface) tokenization was automatically done and then hand-corrected; see [PDT documentation](http://ufal.mff.cuni.cz/pdt2.0/doc/pdt-guide/en/html/ch02.html). Splitting of fused tokens into syntactic words was done automatically during PDT-to-UD conversion. |
| FORM   | Identical to PDT-C form. |
| LEMMA  | Manual selection from possibilities provided by morphological analysis. In the UD conversion, PDT-C lemmas were stripped of the ID numbers distinguishing homonyms, semantic tags and comments; this information is preserved as attributes in the MISC column. |
| UPOS   | Converted automatically from XPOS (via [Interset](https://ufal.mff.cuni.cz/interset)), from the semantic tags in PDT-C lemma, and occasionally from other information available in the treebank. |
| XPOS   | Manual selection from possibilities provided by morphological analysis. |
| FEATS  | Converted automatically from XPOS (via Interset), from the semantic tags in PDT lemma, and occasionally from other information available in the treebank. |
| HEAD   | Original PDT-C annotation is manual. Automatic conversion to UD; human checking of patterns revealed by automatic consistency tests. |
| DEPREL | Original PDT-C annotation is manual. Automatic conversion to UD; human checking of patterns revealed by automatic consistency tests. |
| DEPS   | Generated from the basic UD tree and additional annotation from the original PDT-C. |
| MISC   | Information about token spacing taken from PDT-C annotation. Lemma / word sense IDs, semantic tags and comments on meaning moved here from the PDT-C lemma. Some other annotation from PDT-C, such as coreference and functors (for parts of the corpus). |

The original PDT-C has four layers of annotation: word layer, morphological layer,
analytical (surface-syntactic) layer, and tectogrammatical (deep-syntactic) layer;
they are also referred to as w-, m-, a-, and t-layer. Until UD release 2.11, the
conversion was based only on the first three layers. From release 2.12 on, the
conversion procedure also uses information from the t-layer. Note that this layer
of annotation is not available for the entire treebank.
Sentences for which the t-layer was available can be recognized by the sentence-
level comment "Tectogrammatical annotation available." Some attributes specific
to the t-layer are ported to the MISC column of the CoNLL-U file:

* Functor ... The tectogrammatical functor of this node w.r.t. its parent in the
  t-tree. It often corresponds to the parent in the UD tree but it is not always
  the case.
* Entity ... Coreference annotation in the [CorefUD](https://ufal.mff.cuni.cz/corefud)
  format. While the format could be also used for named entity annotation, named
  entities are annotated only if it is needed for coreference.
* Bridging ... Annotation of bridging relations in the CorefUD format.

Furthermore, conversion of syntactic annotation may occasionally differ from what
it would look like without the tectogrammatical input. This is especially true of
the enhanced dependency graph.


# Acknowledgments

We wish to thank all of the contributors to the original PDT-C annotation effort,
including Jan Hajič, Eduard Bejček, Alevtina Bémová, Eva Buráňová, Eva Fučíková,
Eva Hajičová, Jiří Havelka, Jaroslava Hlaváčová, Petr Homola, Pavel Ircing, Jiří Kárník,
Václava Kettnerová, Natalia Klyueva, Veronika Kolářová, Lucie Kučová, Markéta Lopatková,
David Mareček, Marie Mikulová, Jiří Mírovský, Anna Nedoluzhko, Michal Novák, Petr Pajas,
Jarmila Panevová, Nino Peterek, Lucie Poláková, Martin Popel, Jan Popelka, Jan Romportl,
Magdaléna Rysová, Jiří Semecký, Petr Sgall, Johanka Spoustová, Milan Straka, Pavel Straňák,
Pavlína Synková, Magda Ševčíková, Jana Šindlerová, Jan Štěpánek, Barbora Štěpánková,
Josef Toman, Zdeňka Urešová, Barbora Vidová Hladká, Daniel Zeman, Šárka Zikánová,
Zdeněk Žabokrtský, and many other contributors (technical support, guidelines, annotators)
– they are listed in the [Credits](https://ufal.mff.cuni.cz/pdt-c/credits)
page of the project website.

## References

* Jan Hajič, Eduard Bejček, Jaroslava Hlaváčová, Marie Mikulová, Milan Straka,
  Jan Štěpánek, and Barbora Štěpánková. 2020. Prague Dependency Treebank –
  Consolidated 1.0.
  In: Proceedings of the 12th Conference on Language Resources and Evaluation
  (LREC 2020), Marseille, France, pp. 5208-5218.
  https://aclanthology.org/2020.lrec-1.641.pdf
* Jan Hajič, Eduard Bejček, Alevtina Bémová, Eva Buráňová, Eva Fučíková,
  Eva Hajičová, Jiří Havelka, Jaroslava Hlaváčová, Petr Homola, Pavel Ircing,
  Jiří Kárník, Václava Kettnerová, Natalia Klyueva, Veronika Kolářová, Petr Pajas,
  Jarmila Panevová, Nino Peterek, Lucie Poláková, Martin Popel, Jan Popelka,
  Jan Romportl, Magdaléna Rysová, Jiří Semecký, Petr Sgall, Johanka Spoustová,
  Milan Straka, Pavel Straňák, Pavlína Synková, Magda Ševčíková, Jana Šindlerová,
  Jan Štěpánek, Barbora Štěpánková, Josef Toman, Zdeňka Urešová, Barbora Vidová Hladká,
  Daniel Zeman, Šárka Zikánová, Zdeněk Žabokrtský. 2024.
  Prague Dependency Treebank – Consolidated 2.0 (PDT-C 2.0).
  Data/software, LINDAT/CLARIAH-CZ digital library, Praha, Czechia,
  [http://hdl.handle.net/11234/1-5813](http://hdl.handle.net/11234/1-5813).


# Changelog

* 2025-05-15 v2.16
  * Repository renamed from UD_Czech-PDT to UD_Czech-PDTC.
  * Source data is now PDT-C 2.0 (previously it was 1.0).
    * Large amount of data added. Previously only the core PDT part was converted to UD. Now there is also PCEDT, PDTSC, and Faust.
  * Adjectives heading clauses are acl(:relcl) rather than amod.
  * Fixed attachment of bracketed punctuation.
  * Fixed multiword expressions need the ExtPos feature.
  * Fixed: demonstratives with clauses: det --> nmod.
  * Fixed: genitive postmodifiers should be nmod (not amod, nummod, det).
  * More generally, non-agreeing postponed determiners are now mostly nmod.
  * No longer distinguishing flat:foreign from flat.
* 2024-11-15 v2.15
  * Nouns no longer distinguish Polarity. Negative nouns have negative lemmas.
  * Conditional auxiliary "by" does not have Person (besides 3, it could be also 2).
  * Short forms of adjectives now have Degree=Pos (instead of no Degree).
  * Disambiguated NumType=Mult,Sets.
  * Fixed conversion of "Cz" tags from PDT (not interrogative DET but cardinal NUM).
* 2024-05-15 v2.14
* 2024-03-28 CorefUD 1.2
  * Improved distinction between adverbial predicates (with copula) and adverbial modifiers.
  * Coreference annotation: If a bracket is in mention span, the paired bracket is added too, if possible.
  * More restrictive use of orphans and empty nodes: Not in non-verbal coordinated sentences.
  * Fixed crossing coreference mentions.
  * Fixed treatment of "by" in aux/cop chains.
  * Improved form and position of abstract predicates in gapping.
* 2023-11-15 v2.13
  * Removed NumValue from all Czech UD treebanks.
  * Pseudo-existential "být" with oblique/adverbial modifiers changed to copula.
* 2023-05-15 v2.12
  * Source data switched from PDT 3.0 to PDT-C 1.0.
    * Underlying text data is the same.
    * Changed some aspects of lemmatization, including LId and other attributes in MISC.
    * Somewhat different XPOS tag set.
    * UD features: now all verbs have Aspect; minor changes at various other places.
    * Foreign words are now systematically tagged X (previously, many of them had descriptive UPOS tags).
  * The tectogrammatical (t-) layer of source annotation is now used for documents for which it is available.
    * Sentences converted with the help of t-layer have the comment "Tectogrammatical annotation available."
    * There are more enhanced dependency relations and empty nodes.
    * The MISC column contains CorefUD-style annotation of coreference (now also in the UD release).
    * The MISC column contains tectogrammatical functors.
  * Temporary fix of double subjects (second subject converted to dep).
    In the long run, the cause should be found and fixed upstream.
  * Added the enhanced relation subtype nsubj:xsubj.
* 2023-02-24 CorefUD 1.1
  * Removed superfluous empty nodes #Rcp, #Cor, #QCor.
  * Removed empty nodes depending on the artificial 0:root.
  * "Bych/bys/by/bychom/byste" in MWTs no longer breaks mention spans.
  * Improved guessing of pronominal forms for empty nodes.
  * Functors added also to non-empty nodes.
* 2022-05-15 v2.10
  * Added VerbForm=Part|Voice=Pass to long forms of passive participles.
  * Added VerbForm=Vnoun to verbal nouns.
  * The verb 'být' is now AUX in all contexts.
  * Merged PRON/DET 'sám', 'samý'.
* 2022-04-06 CorefUD 1.0
  * Fixed bug: Distinction between clauses and nominals.
  * Fixed bug: Gapping empty nodes vs. coreference empty nodes.
* 2021-05-15 v2.8
  * Fixed bug: SpaceAfter=No should not occur at the end of paragraph.
  * "§" is now SYM instead of NOUN.
  * Fixed recognition of clauses with passive participles (ADJ).
* 2021-03-11 CorefUD 0.1
  * First release of the coreference annotation together with UD morphology and syntax in the CorefUD collection.
  * Unlike the main releases for UD, CorefUD uses the tectogrammatical layer of PDT and does not include the PDT sentences that lack this layer.
* 2020-11-15 v2.7
  * Fixed bug: question marks were replaced by asterisks.
  * Adjusted treatment of double lemmas like "m`metr".
* 2020-05-15 v2.6
  * Genitive, dative and instrumental nominals are now considered oblique.
  * Added enhanced relations with case information.
  * Added enhanced relations around relative clauses.
  * Added enhanced external subjects in control verb constructions.
  * Added empty nodes to enhanced graphs (but orphans are just converted to dep).
* 2019-05-15 v2.4
  * Modified conversion: nouns do not have objects.
  * Fixed punctuation attachment.
  * Fixed "a to", "to jest" and other expressions.
* 2018-11-15 v2.3
  * Bug fix: conditional "by" should be attached as 'aux', not 'aux:pass'.
  * Flat name structures extended to titles and occupations.
  * Added LDeriv for passive participles (the infinitive of the source verb).
* 2018-04-15 v2.2
  * Repository renamed from UD_Czech to UD_Czech-PDT.
  * Added enhanced representation of dependencies propagated across coordination.
    The distinction of shared and private dependents is derived deterministically from the original Prague annotation.
  * Fixed computation of the LDeriv MISC attribute.
* 2017-11-15 v2.1
  * Retagged pronouns “každý” and “kterýžto”.
  * Prepositional objects are now “obl:arg” instead of “obj”.
  * Instrumental phrases for demoted agents in passives are now “obl:agent”.
* 2017-03-01 v2.0
  * Converted to UD v2 guidelines.
  * Reconsidered PRON vs. DET. Extended PronType and Poss.
  * Improved advmod vs. obl distinction.
  * L-participles are verbs, other participles are adjectives.
  * Removed style flags from lemmas.
* 2016-05-15 v1.3
  * Fixed adverbs that were attached as nmod; correct: advmod.
  * Copulas with clausal complements are now heads.
  * Improved conversion of AuxY.
  * Relation of foreign prepositions changed to foreign.
* 2015-11-15 v1.2
  * Conversion procedure rewritten again (may result in minor differences in
    borderline cases)
  * Only one “root” relation per tree now enforced; some bugs around root fixed
  * The “name” relation goes now always left-to-right (in UD 1.1 it was family-
    to-given name)
  * Fixed bug with numeral-noun swapping that destroyed coordinations of
    numbers and caused the “conj” relation to go right-to-left
  * Fixed minor bugs around subordinating conjunctions
  * Changed dependency relation of reflexive pronouns attached to inherently
    reflexive verbs from compound:reflex to expl
  * Applied heuristics to distinguish at least some iobj from dobj
  * Fixed bugs around xcomp (future infinitives and subjects attached to
    controlled verbs)
* 2015-05-15 v1.1
  * Conversion procedure completely rewritten
  * Improved heuristics to distinguish DET and PRON
  * Improved treatment of comparative complements (conjunctions “než” and “jako”)
  * Remaining lemma extensions moved from LEMMA to MISC



<pre>
=== Machine-readable metadata (DO NOT REMOVE!) ================================
Data available since: UD v1.0
License: CC BY-NC-SA 4.0
Includes text: yes
Genre: news reviews nonfiction academic spoken social
Lemmas: converted from manual
UPOS: converted from manual
XPOS: manual native
Features: converted from manual
Relations: converted from manual
Contributors: Zeman, Daniel; Hajič, Jan; Bémová, Alevtina; Buráňová, Eva; Hajičová, Eva; Havelka, Jiří; Hlaváčová, Jaroslava; Kárník, Jiří; Kolářová, Veronika; Kučová, Lucie; Lopatková, Markéta; Mikulová, Marie; Mírovský, Jiří; Nedoluzhko, Anna; Novák, Michal; Pajas, Petr; Panevová, Jarmila; Sgall, Petr; Straka, Milan; Ševčíková, Magda; Štěpánek, Jan; Štěpánková, Barbora; Urešová, Zdeňka; Vidová Hladká, Barbora; Žabokrtský, Zdeněk
Contributing: elsewhere
Contact: zeman@ufal.mff.cuni.cz
===============================================================================
</pre>
