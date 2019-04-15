<h3 id="cancer">Cancers</h3>

Detects potential cancer disease terms such as adenocarcinoma carcinomatosis. Extra features that can be found by the annotator include: the actual name of the cancer, measurement, cancer grade, site, date, and modality.

<h4>Configurations</h4>

<table>
<caption>Configurations</caption>
<tr>
<th>Configuration</th>
<th>Values</th>
<th>Description</th>
</tr>
<tr>
<td>library</td>
<td>
<ul>
  <li>umls.2016AA <i>(deprecated - will be removed in 2019)</i></li>
  <li>umls.2017AA</li>
  <li>umls.2018AA</li>
  <li>umls.latest</li>
</ul>
</td>
<td>Defines the version of the UMLS library that is used when annotating unstructured data.  The value <q>umls.latest</q> is used to indicate the latest version of the available UMLS libraries (2018AA).  It is also the default value for the <b>library</b> configuration.</td>
</tr>
</table>

<h4>Annotation Types</h4>

*  aci.IcaCancerDiagnosisInd

###### aci.IcaCancerDiagnosisInd

<table>
<caption>aci.IcaCancerDiagnosisInd</caption>
<tr><th>__Feature__</th><th>__Description__</th></tr>
</tr><td>begin</td><td>The start position of the annotation as a character offset into the text. The smallest possible start position is 0.</td></tr>
<tr><td>end</td><td>The end position of the annotation as character offset into the text. The end position points at the first character after the annotation, such that end-begin equals the length of the coveredText.</td></tr>
<tr><td>coveredText</td><td>The text covered by an annotation as a string.</td></tr>
<tr><td>type</td><td>aci.IcaCancerDiagnosisInd</td></tr>
<tr><td>modality</td><td>Potenial values are: <q>positive</q> and <q>negative</q>.  This based on whether the patient has or does not have the cancer identified.</td></tr>
<tr><td>sectionSurfaceForm</td><td>Medical documents have many sections such as patient's information, previous medical history, family history, etc.  The covered text that identifies which section of the document that spans the annotation. The default value of this feature is <q>document</q>.</td></tr>
<tr><td>sectionNormalizedName</td><td>The normalized term for the section.</td></tr>
<tr><td>Cancer</td><td><table role="presentation"><tbody>
  <tr><td>begin</td><td>The start position of the annotation as a character offset into the text. The smallest possible start position is 0.</td></tr>
  <tr><td>end</td><td>The end position of the annotation as character offset into the text. The end position points at the first character after the annotation, such that end-begin equals the length of the coveredText.</td></tr>
  <tr><td>type</td><td>aci.Cancer</td></tr>
  <tr><td>coveredText</td><td>The text covered by an annotation as a string.</td></tr>
  <tr><td>cancerSurfaceForm</td><td>Covered text that represents the cancer.   For example, in the text <q>He has lung cancer</q>, the cancerSurfaceForm is <q>lung cancer</q>.</td></tr>
  <tr><td>cancerNormalizedName</td><td>Normalized name for the cancer from the UMLS dictionary   For example, in the text <q>He has lung cancer</q>, the cancerSurfaceForm is <q>primary malignant neoplasm of lung</q>.</td></tr>
  <tr><td>ccsCode</td><td>CCS stands for Clinical Classification System, used to categorize diagnosis and procedures such that it can be used for further analysis.</td></tr>
  <tr><td>hccCode</td><td>HCC stands for Hierarchical Condition Categories and primarily used by Medicare and Medicaid.</td></tr>
  <tr><td>icd9Code</td><td>ICD stands for International Classification of Diseases.  The number 9 is a revision number for this code set.</td></tr>
  <tr><td>icd10Code</td><td>ICD stands for International Classification of Diseases.  The number 10 is a revision number for this code set.</td></tr>
  <tr><td>snomedConceptId</td><td>Numerical code provided by the SNOMED dictionaries that represents the cancer.</td></tr>
  <tr><td>cui</td><td>UMLS Concept Unique ID (CUI). CUIs are used to uniquely identify concepts across different UMLS sources. Depending on the source of the cancer information, this value may not be available.</td></tr>
  <tr><td>morphologyCode</td><td>A value that describes the behavior of cancer from malignant to benign.</td></tr>
  <tr><td>behavior</td><td>The code represents the type of growth such as benign, malignant, in situ, or uncertain.  This code only applies to cancer related disease.
  <table role="presentation"><tbody>
    <tr><td>0</td><td>Benign</td></tr>
    <tr><td>1</td><td>Unknown (uncertain if benign or malignant)</td></tr>
    <tr><td>2</td><td>Insitu</td></tr>
    <tr><td>3</td><td>Malignant (primary)</td></tr>
    <tr><td>6</td><td>Malignant (metastatic or secondary site)</td></tr>
    <tr><td>9</td><td>Malignant (uncertain if primary or metastatic)</td></tr>
    </tbody></table></td></tr>
  <tr><td>behaviorSource</td><td>A code that will either come from morphology code, icd 9 code, or icd 10 code.</td></tr>
</tbody></table></td><tr>
<tr><td>date</td><td><table role="presentation"><tbody>
  <tr><td>begin</td><td>The start position of the annotation as a character offset into the text. The smallest possible start position is 0.</td></tr>
  <tr><td>end</td><td>The end position of the annotation as character offset into the text. The end position points at the first character after the annotation, such that end-begin equals the length of the coveredText.</td></tr>
  <tr><td>type</td><td>aci.Date</td></tr>
  <tr><td>coveredText</td><td>The text covered by an annotation as a string.</td></tr>
  <tr><td>dateInMilliseconds</td><td>It is a java.util.Calendar date and is the difference, measured in milliseconds, between the date of the event and midnight, January 1, 1970 UTC.</td></tr>
</tbody></table></td></tr>
<tr><td>measurement</td><td><table role="presentation"><tbody>
  <tr><td>begin</td><td>The start position of the annotation as a character offset into the text. The smallest possible start position is 0.</td></tr>
  <tr><td>end</td><td>The end position of the annotation as character offset into the text. The end position points at the first character after the annotation, such that end-begin equals the length of the coveredText.</td></tr>
  <tr><td>type</td><td>aci.Measurement</td></tr>
  <tr><td>coveredText</td><td>The text covered by an annotation as a string.</td></tr>
  <tr><td>dimension</td><td>Type of mesurement. For example, in the text <q>4.3mm tumor</q>, the dimension of measurement is <q>length</q>.</td></tr>
</tbody></table></td></tr>
<tr><td>CancerGrade</td><td><table role="presentation"><tbody>
  <tr><td>begin</td><td>The start position of the annotation as a character offset into the text. The smallest possible start position is 0.</td></tr>
  <tr><td>end</td><td>The end position of the annotation as character offset into the text. The end position points at the first character after the annotation, such that end-begin equals the length of the coveredText.</td></tr>
  <tr><td>coveredText</td><td>The text covered by an annotation as a string.</td></tr>
  <tr><td>type</td><td>aci.CancerGrade</td></tr>
  <tr><td>gradeValue</td><td>The value of the grade.</td></tr>
</tbody></table></td></tr>
<tr><td>site</td><td><table role="presentation"><tbody>
  <tr><td>begin</td><td>The start position of the annotation as a character offset into the text. The smallest possible start position is 0.</td></tr>
  <tr><td>end</td><td>The end position of the annotation as character offset into the text. The end position points at the first character after the annotation, such that end-begin equals the length of the coveredText.</td></tr>
  <tr><td>coveredText</td><td>The text covered by an annotation as a string.</td></tr>
  <tr><td>type</td><td>aci.SiteInd</td></tr>
  <tr><td>gradeValue</td><td>The value of the grade.</td></tr>
  <tr><td>siteNormalizedName</td><td>The normalized name for the site from UMLS.</td></tr>
  <tr><td>compound</td><td>Whether this a multi-site term.</td></tr>
  <tr><td>snomedConceptId</td><td>Numerical code provided by the SNOMED dictionaries that represents the site.</td></tr>
</tbody></table></td></tr>
</table>