# K-Anonymity

K-Anonymity is one of the integrated Data Anonymization methods in HANA Cloud that allows a consumer to gain valid insights from data while the privacy of individuals is protected. 

In HANA Cloud, anonymization takes place during runtime, so the consumer always gets the most up-to-date data through the anonymization view created on the original data.

## How does K-Anonymity work?

The original data gets categorized into three different categories:

- Identifying information (such as names or ID's) that allow you to directly identify an individual.
- Quasi-identifying information (such as gender, age or birthplace) that do not allow an individual to be identified directly. This might only be possible by combing severel quasi-identifiers. 
- Sensitive data (e.g. illness or salary) of an individual should not be disclosed.

The goal is to create groups of the same quasi-identifier characteristics with a size of k to hide individuals of the same chareteristics in it. The minimum size of k is 2.

To reach this goal it is necessary to remove the identifiers from the data. But this is mostly not enough to save an individual from reidentification. So it is necessary to build hierarchies for the quasi-identifiers that make the information less specific. The sensitive information is passed on unchanged to allow analysis.

## Example of hierarchies for quasi-identifiers

To illustrate the principle of hierarchies and the quasi-identifiers, here is a short example:

The following list shows the place of residence of an individual and the way in which this can be generalized to a higher level.

_City_ | _State_ | _Country_ | _Continent_ |
-|-|-|-|
Munich | Bavaria | Germany | Europe |
Frankfurt am Main | Hesse | Germany | Europe |

Here an individual living in Munich can not be distinguished from an individual living in Frankfurt, if this information gets generealized two times to Germany.

Further information:

[SAP HANA Cloud, SAP HANA Database Data Anonymization Guide](https://help.sap.com/viewer/2f789e82e97d4f4e9416547abfbd012e/2021_01_QRC/en-US/a66e8541c4004f048630f8a55f67ad37.html)

[Back to Hands-On Overview](./Overview.md)
