---

copyright:
  years: 2011, 2019
lastupdated: "2019-04-12"

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

# Lab Values
{: #lab_values}

The purpose of the Lab Value annotator is to annotate the value associated with lab measurements and tests. The annotator uses lab measurements and test defined in the Logical Observation Identifiers Names and Codes (LOINC) database. This database is a universal standard for identifying medical laboratory observations. The user can provide their surface forms for lab measurements and tests by using the labTypess whitelist described in the Customization section. Only the value of the measurement or test is covered by the annotation's span. To determine what test or measurement is associated with the value use the labTypeNormalizedName and labTypeSurfaceForm features in the annotation. The Lab Value annotator is written to only handle single values or fractional values composed of two single values.
{:shortdesc}

Examples:

B.P. 118/76 (sitting) 120/80 (standing).

```javascript
"LabValueInd": [
   {
       "type": "aci.LabValueInd",
       "begin": 5,
       "end": 11,
       "coveredText": "118/76",
       "loincId": "18684-1",
       "lowValue": "76",
       "dateInMilliseconds": " ",
       "labTypeSurfaceForm": "B.P.",
       "labTypeNormalizedName": "Blood pressure",
       "labValue": "118",
       "position": "sitting"
   },
   {
       "type": "aci.LabValueInd",
       "begin": 22,
       "end": 28,
       "coveredText": "120/80",
       "loincId": "18684-1",
       "lowValue": "80",
       "dateInMilliseconds": " ",
       "labTypeSurfaceForm": "B.P.",
       "labTypeNormalizedName": "Blood pressure",
       "labValue": "120",
       "position": "standing"
   }
]
```

pulse: 84

```javascript
"LabValueInd": [
     {
         "type": "aci.LabValueInd",
         "begin": 7,
         "end": 9,
         "coveredText": "84",
         "dateInMilliseconds": " ",
         "labTypeSurfaceForm": "pulse",
         "labTypeNormalizedName": "pulse",
         "labValue": "84"
     }
 ]
```

temperature 20.1 degrees celsius

```javascript
"LabValueInd": [
     {
         "type": "aci.LabValueInd",
         "begin": 12,
         "end": 16,
         "coveredText": "20.1",
         "loincId": "8310-5",
         "dateInMilliseconds": " ",
         "labTypeSurfaceForm": "temperature",
         "labTypeNormalizedName": "Body temperature",
         "labValue": "20.1",
         "measurementUnit": [
             {
                 "coveredText": "degrees celsius",
                 "end": 32,
                 "type": "aci.MeasurementUnit",
                 "begin": 17,
                 "dimension": "temperature",
                 "compound": "false"
             }
         ]
     }
 ]
```

<h4>Configurations</h4>

<table>
<caption>Configurations</caption>
<tr>
<th>Configuration</t>
<th>Values</th>
<th>Description</th>
</tr>
<tr>
<td>library</td>
<td>
<ul>
  <li>umls.latest</li>
  <li>umls.2018AA</li>
  <li>umls.2017AA</li>
  <li>umls.2016AA <i>(deprecated - will be removed in 2019)</i></li>
</ul>
</td>
<td>Defines the version of the UMLS library that is used when annotating unstructured data.  The value <q>umls.latest</q> is used to indicate the latest version of the available UMLS libraries (2018AA).  It is also the default value for the <b>library</b> configuration.
</td>
</tr>
</table>

<h4>Annotation Types</h4>

* aci.LabValueInd

###### aci.LabValueInd

<table>
<caption>aci.LabValueInd</caption>
<tr><th>__Feature__</th><th>__Description__</th></tr>
</tr><td>begin</td><td>The start position of the annotation as a character offset into the text. The smallest possible start position is 0.</td></tr>
<tr><td>end</td><td>The end position of the annotation as character offset into the text. The end position points at the first character after the annotation, such that end-begin equals the length of the coveredText.</td></tr>
<tr><td>coveredText</td><td>The text covered by an annotation as a string.</td></tr>
<tr><td>type</td><td>aci.LabValueInd</td></tr>
<tr><td>date</td><td>Indicates the date that is related to the event.  For instance, in a patient's medical form, this date may indicate the date of surgery, or the date of last diagnosis.  The value of date is detected from the date that is nearest to the text that is annotated.</td></tr>
<tr><td>dateInMilliseconds</td><td>It is a java.util.Calendar date and is the difference, measured in milliseconds, between the date of the event and midnight, January 1, 1970 UTC.</td></tr>
<tr><td>dateSource</td><td>Indicates where in the document or text the date value is identified. For example, <q>sentence</q> is one possible option for dateSource.</td></tr>
<tr><td>labTypeSurfaceForm</td><td>Covered text that represents the lab.   For example, in the text <q>Upright BP is 120/80 mmHg</q>, the labTypeSurfaceForm is <q>BP</q>.</td></tr>
<tr><td>labTypeNormalizedName</td><td>Normalized name for the lab from the UMLS dictionary or user provided whitelist.   For example, in the text <q>Upright BP is 120/80 mmHg</q>, the labTypeNormalizedName is <q>Blood pressure</q>.</td></tr>
<tr><td>labValue</td><td>Value of the lab type.  For example, in the text <q>Upright BP is 120/80 mmHg</q>, the lab value is 120/80.</td></tr>
<tr><td>loincId</td><td>LOINC stands for Logical Observations Identifiers, Names, Codes.  The value for this feature comes from UMLS.</td></tr>
<tr><td>lowValue</td><td>Minimum value for the lab when the lab value falls within a range or expected to be at minimum value.  For example, in the text <q>Upright BP is 120/80 mmHg</q>, the low value is 80.</td></tr>
<tr><td>measurementUnit</td><td><table role="presentation"><tbody>
  <tr><td>begin</td><td>The start position of the annotation as a character offset into the text. The smallest possible start position is 0.</td></tr>
  <tr><td>end</td><td>The end position of the annotation as character offset into the text. The end position points at the first character after the annotation, such that end-begin equals the length of the coveredText.</td></tr>
  <tr><td>coveredText</td><td>The text covered by an annotation as a string.</td></tr>
  <tr><td>type</td><td>aci.MeasurementUnit</td></tr>
  <tr><td>dimension</td><td>Type of mesurement. For example, in the text <q>Upright BP is 120/80 mmHg</q>, the dimension of measurement is <q>pressure</q>.</td></tr>
  <tr><td>compound</td><td>Value of <q>true</q> when there is a numerator or denomenator present.</td></tr>
  <tr><td>numerator</td><td>The first value of a compound measurement.</td></tr>
  <tr><td>denomenator</td><td>The second value of a compound mesurement.</td></tr>
</tbody></table></td></tr>
<tr><td>position</td><td>Position of the patient while a lab test was performed.  For example, in the text <q>Upright BP is 120/80 mmHg</q>, the position is Upright.</td></tr>
</table>
