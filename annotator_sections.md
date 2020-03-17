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

# Sections
{: #_sections}

The section annotator is used to identify the section of a document where concepts are found. For example, a patient's discharge summary may contain a <q>Family History</q> section identifying medical diagnoses of the patient's parents. In some instances, this information may not be relevant for a particular use case. Using the section annotator, annotations identified as belonging to the <q>Family History</q> section may be filtered out.
{:shortdesc}

The section annotator provides a set of predefined section titles based on the [Logical Observation Identifiers Names and Codes (LOINC)](https://loinc.org/) vocabulary. In addition to the predefined section titles, section headings are also identified based on a few simple formatting rules:

1. If a heading is in all uppercase letters followed by a ":", such as "VACCINES:", the heading will be treated as a section header.
2. If a section title is followed or preceded by all uppercase letters (with "/" in between), both the section title and the uppercase portion is considered the section header. If uppercase letters follow the dictionary entry, the uppercase portion may include parentheses. Examples include "RELEVANT/FamilyHistory:" and "Family History/(RELEVANT):".
3. By default, a section will only be identified if the section title starts at the beginning of a line. To identify sections when the title appears later in the text, use the **sections_can_start_anywhere** configuration parameter.

A section includes all the text between two section headings. Annotations that exist within the section will be annotated with  the section information in the **sectionNormalizedName** and **sectionSurfaceForm<** fields.

<h4>Annotation Types</h4>

* Section

<h4>Configurations</h4>

<table>
<tr>
<th>Configuration</t>
<th>Values</th>
<th>Description</th>
</tr>
<tr>
<td>include_covered\_text</td>
<td>true/false</td>
<td>When true, the coveredText feature for the section annotation is returned. When false _(default)_, the coveredText feature is not returned.</td>
</tr>
<tr>
<td>turn_off_internal\_triggers</td>
<td>true/false</td>
<td>When true, the predefined section titles are not used. When false _(default)_, the predefined section titles are used to identify sections.</td>
</tr>
<tr>
<td>sections_can_start\_anywhere</td>
<td>true/false</td>
<td>When true, section titles can be located in any portion of the text, not just at the beginning of a line. When false _(default)_, section titles are only considered when beginning a line.</td>
</tr>
</table>

###### Section

<table>
<caption>Section</caption>
<tr><th>__Field__</th><th>__Description__</th></tr>
</tr><td>begin</td><td>The start position of the annotation as a character offset into the text. The smallest possible start position is 0.</td></tr>
<tr><td>end</td><td>The end position of the annotation as character offset into the text. The end position points at the first character after the annotation, such that end-begin equals the length of the coveredText.</td></tr>
<tr><td>coveredText</td><td>The text covered by an annotation as a string.</td></tr>
<tr><td>type</td><td>Annotation type for Section</td></tr>
<tr><td>trigger</td><td><table role="presentation"><tbody>
  <tr><td>begin</td><td>The start position of the annotation as a character offset into the text. The smallest possible start position is 0.</td></tr>
  <tr><td>end</td><td>The end position of the annotation as character offset into the text. The end position points at the first character after the annotation, such that end-begin equals the length of the coveredText.</td></tr>
  <tr><td>coveredText</td><td>The text that initiated the section annotation.</td></tr>
  <tr><td>source</td><td>The dictionary source used to identify the section. For the predefined section titles, the value will be `internal`.</td></tr>
</tbody></table></td></tr>
</table>

### Sample Response

Sample response from the section annotator for the text: `Family history:\nMaternal history of diabetes.`

This example also show a concept that was annotated with the **sectionSurfaceForm** and **sectionNormalizedName** fields.

```
{
  "unstructured": [
    {
      "text": "Family history:\nMaternal history of diabetes.",
      "data": {
        "concepts": [
          {
            "cui": "C0011847",
            "preferredName": "Diabetes",
            "semanticType": "dsyn",
            "source": "umls",
            "type": "umls.DiseaseOrSyndrome",
            "begin": 36,
            "end": 44,
            "coveredText": "diabetes",
            "loincId": "LP128793-9,LA10529-8,MTHU040702",
            "sectionNormalizedName": "family history",
            "vocabs": "LNC,MTH,LCH_NW,OMIM",
            "sectionSurfaceForm": "Family history"
          }
        ],
        "sections": [
          {
            "trigger": {
              "sectionNormalizedName": "family history",
              "type": "aci.SectionTrigger",
              "begin": 0,
              "end": 14,
              "coveredText": "Family history",
              "source": "internal"
            },
            "type": "aci.Section",
            "begin": 0,
            "end": 45
          }
        ]
      }
    }
  ]
}
```
