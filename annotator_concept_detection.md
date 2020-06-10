---

copyright:
  years: 2011, 2019
lastupdated: "2019-04-12"

keywords: annotator clinical data, clinical data, annotation

subcollection: wh-acd

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:deprecated: .deprecated}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# Concept Detection
{: #concept_detection}

The concept detection service detects medical concepts from unstructured data. The service provides concepts based on the Unified Medical Language System (UMLS). As of the 2018AA version of the UMLS library, the consumers can elect to have a set of [medical codes](/docs/wh-acd?topic=wh-acd-medical_codes#medical_codes) associated with the UMLS concepts by specifying the optional configuration parameter to return the medical codes. When medical codes are requested, the UMLS concept annotations from concept detection will include the applicable medical codes as metadata within the annotations.
{:shortdesc}

### Expanded Concepts

Concept detection provides an _expanded_ option that tries to find UMLS concepts over spans of text that are not strictly defined in the UMLS dictionary that ships with {{site.data.keyword.wh-acd_short}}.  For example, consider the following text:

`The patient broke his leg and hip when he fell outside his home.`

There are two different injuries expressed in this text that we want to capture - broken leg and broken hip.  Neither one will have a dictionary entry that covers the way the concept is expressed.  The **expanded** option tells concept detection to try to find concepts that do not strictly match a known surface form but are present in the text.  In this example, concept detection would return the following concepts with **expanded** set `true`.

```
{
    "cui": "C0159852",
    "preferredName": "Fracture of tibia and fibula",
    "semanticType": "inpo",
    "source": "umls-expanded",
    "sourceVersion": "2018AA",
    "type": "umls.InjuryOrPoisoning",
    "begin": 12,
    "end": 25,
    "coveredText": "broke his leg",
    "icd10Code": "S82.90X?",
    "snomedConceptId": "414293001",
    "vocabs": "MTH,CHV,CCS,ICD9CM,SNOMEDCT_US,ICPC"
}

...

{
    "cui": "C0019557",
    "preferredName": "Hip Fractures",
    "semanticType": "inpo",
    "source": "umls-expanded",
    "sourceVersion": "2018AA",
    "type": "umls.InjuryOrPoisoning",
    "begin": 12,
    "end": 33,
    "coveredText": "broke his leg and hip",
    "loincId": "MTHU020794",
    "icd10Code": "S72.009?",
    "nciCode": "C26794,C35153",
    "snomedConceptId": "5913000,263225007",
    "meshId": "M0010366",
    "vocabs": "MTH,CHV,LNC,CSP,MSH,NCI,AOD,NCI_CTCAE,NDFRT,COSTAR,SNOMEDCT_US,DXP"
}```

Expanded detection will look for diseases, conditions, abnormalities, injuries, and procedures. Expanded detection only works with the UMLS dictionaries that ship with {{site.data.keyword.wh-acd_short}}.  It does not work with custom dictionaries.


<h4>Configurations</h4>

The following table lists parameters of the concept_detection service.

<table>
  <caption>Configurations</caption>
  <tr>
    <th>Configuration</th>
    <th>Values</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>libraries</td>
    <td><ul>
      <li>umls.latest</li>
      <li>umls.2019AA</li>
      <li>umls.2018AA</li>
      <li>umls.2017AA <i>(deprecated - will be removed in 2020)</i></li>
    </ul></td>
    <td>
    Defines the version of the UMLS library that is used when analyzing unstructured data. The value `umls.latest` will reference the latest available version of UMLS within the service. As newer versions of UMLS are made available in the service, `umls.latest` library configurations will automatically leverage the latest available version of UMLS in the service once available. Declaration of a specific version of UMLS is recommended to avoid undesirable changes in output as newer versions of UMLS are made available within the service. Through declaration of a specific version of UMLS, newer versions of UMLS may be evaluated prior to use in production.
    </td>
  </tr>
  <tr>
    <td>inference_rules</td>
    <td></td>
    <td>The name of a derived concept rule set that will be used for deriving additional concepts based on the concepts discovered by the libraries specified.</td>
  </tr>
  <tr>
    <td>filters</td>
    <td></td>
    <td>The name of a concept filter that is used to remove unwanted concepts.</td>
  </tr>
  <tr>
    <td>expanded</td>
    <td>true/false</td>
    <td>When true, the concept detection annotator will attempt to expand concept coverage beyond the surface forms explicitly listed in the specified library.  For example - if <q>broken collarbone</q> is a surface from for C0159658 (Fracture of clavicle), the expanded option would match textual representations of that concept like <q>broke my collarbone</q>.  This option is <i>false</i> by default.</td>
  </tr>
  <tr>
    <td>include_optional_fields</td>
    <td>medical_codes </br> source_vocabularies </td>
    <td>Optional fields that should also be returned for each concept. If not specified, only the libary's default fields will be returned. </td>
  </tr>
  <tr>
    <td>longest_span</td>
    <td>true/false</td>
    <td>When true <i>(default)</i>, only the concept with the longest text span will be returned if there are multiple concepts overlapping the same span of text.</td>
  </tr>
</table>

<h4>Annotation Types</h4>

* Concept

###### Concept

<table>
<tr>
<th>Fields</th>
<th>Description</th>
</tr>
<tr>
<td>cui</td>
<td>Concept Unique ID (CUI). CUIs are used to uniquely identify concepts.</td>
</tr>
</tr>
<tr>
<td>preferredName</td>
<td>Normalized name for the concept.</td>
</tr>
</tr>
<tr>
<td>semanticType</td>
<td>Shorthand version of the UMLS semantic type.</td>
</tr>
</tr>
<tr>
<td>source</td>
<td>The library source used for the detection of the concepts.</td>
</tr>
</tr>
<tr>
<td>sourceVersion</td>
<td>The version of the library source used for the detection of the concepts.</td>
</tr>
</tr>
<tr>
<td>type</td>
<td>The semantic type associated with the concept.</td>
</tr>
<tr>
<td>begin</td>
<td>The start position of the annotation as a character offset into the text. The smallest possible start position is 0.</td>
</tr>
<tr>
<td>end</td>
<td>The end position of the annotation as character offset into the text. The end position points at the first character after the annotation, such that end-begin equals the length of the coveredText.</td>
</tr>
<tr>
<td>coveredText</td>
<td>The text covered by an annotation as a string.</td>
</tr>
<tr>
<td>cptCode</td>
<td>This code represents the type of procedure that is performed. CPT stands for Current Procedural Terminology. This code a standard terminology used by different members of medical society such as physicians, financial administrators, coders, and other organizations. This value is only available when a CPT Codes file is referenced in the profile.</td>
</tr>
<tr>
<td>sourceVocabularies</td>
<td>This provides the list of UMLS source vocabularies that contained the concept. This is provided when the **include_optional_fields** parameter is specified with a value of `source_vocabularies`.</td>
</tr>
</table>


The following optional response fields are provided when the **include_optional_fields** parameter is specified with a value of `medical_codes`.

<table>
<tr>
<th>Fields</th>
<th>Description</th>
</tr>
<tr><td>loincId</td><td>LOINC stands for Logical Observations Identifiers, Names, Codes.  The value for this feature comes from UMLS.</td></tr>
<tr><td>NCI Code </td><td> The <a href="https://www.nlm.nih.gov/research/umls/sourcereleasedocs/current/NCI/">NCI Thesaurus</a> covers vocabulary for cancer-related clinical care, translational and basic research, and public information and administrative activities.  The value for this feature comes from UMLS. </td></tr>
<tr><td>snomedConceptId</td><td>Numerical code provided by the SNOMED dictionaries that represents the cancer.</td></tr>
<tr><td>MeSHId </td><td>The <a href="https://www.nlm.nih.gov/research/umls/sourcereleasedocs/current/MSH/">MeSH thesaurus</a> is a controlled vocabulary used for indexing, cataloging, and searching for biomedical and health-related information and documents.  The value for this feature comes from UMLS.</td></tr>
<tr><td>icd9Code</td><td>ICD stands for International Classification of Diseases.  The number 9 is a revision number for this code set.</td></tr>
<tr><td>icd10Code</td><td>ICD stands for International Classification of Diseases.  The number 10 is a revision number for this code set.</td></tr>
<tr><td>rxNormID</td><td>Also called the RXCUI which is a normalized id that is defined in the RxNorm standard and commonly used amongst different organizations.</td></tr>
</table>

### Sample Response

Sample response from the concept detection annotator for the text: `She is taking Metformin for her type 2 diabetes.`

This example provides the optional medical codes and source vocabularies.

```javascript
{
  "unstructured": [
    {
      "text": "She is taking Metformin for her type 2 diabetes.",
      "data": {
        "concepts": [
          {
            "cui": "C0025598",
            "preferredName": "Metformin",
            "semanticType": "phsu",
            "source": "umls",
            "sourceVersion": "2018AA",
            "type": "umls.PharmacologicSubstance",
            "begin": 14,
            "end": 23,
            "coveredText": "Metformin",
            "rxNormId": "6809",
            "loincId": "LP33332-5,MTHU016062",
            "nciCode": "C61612",
            "snomedConceptId": "372567009,109081006",
            "meshId": "M0013535",
            "vocabs": "LNC,CSP,MSH,RXNORM,MTHSPL,NCI_NCI-GLOSS,CHV,ATC,NCI_FDA,NCI,LCH_NW,USPMG,NDFRT,SNOMEDCT_US,DRUGBANK,VANDF"
          },
          {
            "cui": "C0011860",
            "preferredName": "Diabetes Mellitus, Non-Insulin-Dependent",
            "semanticType": "dsyn",
            "source": "umls",
            "sourceVersion": "2018AA",
            "type": "umls.DiseaseOrSyndrome",
            "begin": 32,
            "end": 47,
            "coveredText": "type 2 diabetes",
            "loincId": "LA10552-0",
            "icd10Code": "E11.9",
            "nciCode": "C26747",
            "snomedConceptId": "44054006",
            "meshId": "M0006155",
            "vocabs": "MTH,NCI_NICHD,LNC,CSP,MSH,HPO,OMIM,COSTAR,CHV,MEDLINEPLUS,NCI,LCH_NW,NDFRT,SNOMEDCT_US,DXP"
          }
        ]
      }
    }
  ]
}
```
