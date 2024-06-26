---
title: "Organising Data with Pandas"
teaching: 45
exercises: 15
---

:::::::::::::::::::::::::::::::::::::: questions 

- What is Pandas and what is it for?
- What is a dataframe?
- How can I use Python and Pandas to create dataframes?
- How can I organise the data presented in a dataframe?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Use the Pandas package in Python and spaCy's dframCy module to organise data in a tabular format.
- Manipulate different types of objects for organisation and analysis.

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::challenge

Using the first item in the ‘modern_classical_ambient_desc_only’ dataset that you worked on in the previous episode, create a dataframe that includes ```token.text``` and ```token.pos_``` values for all of the nouns and proper nouns contained in that text. Make your final output the ```.shape``` attribute of the dataframe, and check this against the results in the last episode.

Then, write a .csv file of this dataframe, titled 'clouds_nouns.csv'

:::::::::::::::hint 

You will need to create a dictionary of annotations and then create a dataframe and filter out columns and rows.

:::::::::::::::

:::::::::::::::::::::solution 

```python
desc_doc = nlp("'Clouds' is a perfectly measured suite of warm and hazy downbeats from Gigi Masin, Marco Sterk (Young Marco), and Johnny Nash recorded in the heart of Amsterdam's red light district over one weekend in April, 2014.It's all about louche vibes and glowing notes, gently absorbing and transducing the buzz of the streets outside the studio's open windows into eight elegantly reserved improvisations segueing between lush ambient drift, dub-wise solo piano pieces, and chiming late night jazz patter. In that sense, there's striking similarities between 'Clouds' and the recent Sky Walking album by Lawrence and co., but where they really go for the looseness, Gaussian Curve keep it supple yet tight, bordering on adult contemporary suaveness anointed with finest hash oil. Imbibe slowly.")
desc_doc_dict = [{
    "text": token.text,
    "pos": token.pos_,
    "tag": token.tag_,
    "dep": token.dep_,
    "head": token.head}
for token in desc_doc]
desc_doc_dict
desc_df = pd.DataFrame.from_records(desc_doc_dict)
desc_pos_df = desc_df.drop(columns=["tag", "dep", "head"])
desc_nouns_df = desc_pos_df[desc_pos_df["pos"].isin(["NOUN", "PROPN"])]
desc_nouns_df
```
```
	text	pos
0	Clouds	NOUN
6	suite	NOUN
11	downbeats	NOUN
13	Gigi	PROPN
14	Masin	PROPN
16	Marco	PROPN
17	Sterk	PROPN
19	Young	PROPN
20	Marco	PROPN
24	Johnny	PROPN
25	Nash	PROPN
29	heart	NOUN
31	Amsterdam	PROPN
34	light	NOUN
35	district	NOUN
38	weekend	NOUN
40	April	PROPN
42	2014.It	PROPN
47	vibes	NOUN
50	notes	NOUN
57	buzz	NOUN
60	streets	NOUN
63	studio	NOUN
66	windows	NOUN
71	improvisations	NOUN
76	drift	NOUN
78	dub	NOUN
82	piano	NOUN
83	pieces	NOUN
88	night	NOUN
89	jazz	NOUN
90	patter	NOUN
94	sense	NOUN
99	similarities	NOUN
102	Clouds	PROPN
107	Sky	PROPN
108	Walking	PROPN
109	album	NOUN
111	Lawrence	PROPN
113	co.	PROPN
122	looseness	NOUN
124	Gaussian	PROPN
125	Curve	NOUN
134	adult	NOUN
136	suaveness	NOUN
140	hash	NOUN
141	oil	NOUN
```
```python
desc_nouns_df.shape
```
```
(47, 2)
```
```python
desc_nouns_df.to_csv("clouds_nouns.csv")
```

:::::::::::::::::::::

:::::::::::::::

::::::::::: keypoints

1. Pandas is a Python library for data manipulation and analysis.
2. You can use Pandas to create dataframes, i.e. data structures consisting of rows and columns from your spaCy ```doc``` and ```list``` objects.
3. You can add or remove columns and rows based on their labels or values and quantitatively sort and analyse the contents.
4. You can also use Pandas to write and export .csv and .tsv files for further manual coding or other manipulation.

::::::::::: 
