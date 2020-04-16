CODE NAME: EUNOMIA

For as long as recent legal system has existed, our legal professionals have kept the tradition of keeping things "traditional".  To speak blunt, outdated text was kept alive in part due to the fear of potential mistakes when bringing in change.
These professions have evolved to be interpreters of the jenga tower of convoluted text that is our written law.

[EUNOMIA] is meant to tackle this problem by representing legal text as structured data, allowing our existing legal system to be equipped with automation capabilities to finally embrace digital governance through brevity.

The format of the data structure is borrowed from the concept of the Justinian codification of 6th century Roman law, [*Corpus Juris Civilis*](https://www.wikiwand.com/en/Corpus_Juris_Civilis), which represented legal text in
```1. persons
2. things
3. actions
```

This concept was adapted again in the 19th century to produce the [*Napoleonic Code*](https://www.wikiwand.com/en/Napoleonic_Code) representing legal text in

```1. persons
2. property
3. acquisition of property
4. civil procedure
```

While these codes were meant to modernize feudal laws where legal system was disconnected, the current generation suffers a vastly more complicated issue of being too verbose.  It is said in *Déclaration des droits de l'homme et du citoyen de 1789 (Declaration of the Rights of Man and of the Citizen)* Article VI:
```The law is the expression of the [general will](https://www.wikiwand.com/en/General_will). All the citizens have the right of contributing personally or through their representatives to its formation. It must be the same for all, either that it protects, or that it punishes. All the citizens, being equal in its eyes, are equally admissible to all public dignities, places, and employments, according to their capacity and without distinction other than that of their virtues and of their talents.```

Similarly, the United Nations [Universal Declaration of Human Rights](https://www.un.org/en/universal-declaration-human-rights/index.html) Article 21.,

```(1) Everyone has the right to take part in the government of his country, directly or through freely chosen representatives.
(2) Everyone has the right of equal access to public service in his country.
(3) The will of the people shall be the basis of the authority of government; this will shall be expressed in periodic and genuine elections which shall be by universal and equal suffrage and shall be held by secret vote or by equivalent free voting procedures.```

Many modern legal systems necessarily require highly trained legal professionals to interpret the legal text which is directly prohibitive for equal participation by the public/general will in the formation and remediation of law.

[EUNOMIA] attempts to represent the legal text in the following elements:
```1. Actor
2. Actee
3. Action
4. Condition
```

The core elements which is coined as a [NOME] would consist of elements 1-3. Element 4, the Condition, would consist again of [NOME(s)] and as deeply nested as required.  The parent [NOME] must only apply when all conditions set out in the condition NOME(s) is true.

To expand and represent as a data object:
```{
	"actor" : {
		"value" : *actor name*,
		"negation" : *boolean data*
	},
	"actee" : {
		"value" : *actee name*,
		"negation" : *boolean data*
	},
	"action" : {
		"value" : "action name",
		"negation" : *boolean data*,
		"object" : *array of object(s)*
	},
	"condition" : NOME OBJECT(s)
}
```

<!---
As example, the [Canadian Charter of Rights and Freedoms](https://www.wikiwand.com/en/Canadian_Charter_of_Rights_and_Freedoms) Section 1:
```The Canadian Charter of Rights and Freedoms guarantees the rights and freedoms set out in it subject only to such reasonable limits prescribed by law as can be demonstrably justified in a free and democratic society.```

could be structured into:
```{
	"actor" : {
		"value" : "The Canadian Charter of Rights and Freedoms",
		"negation" : False
	},
	"actee" : {
		"value" : "everyone???",
		"negation" : False
	},
	"action" : {
		"value" : "guarantee",
		"negation" : False,
		"object" : "Right"
	},
	"condition" : {

	}

}
-->

As example, the Canadian [Food and Drugs Act (R.S.C., 1985, c. F-27) Part I section 3 (1)](https://www.laws-lois.justice.gc.ca/eng/acts/F-27/page-2.html#h-234054):
```No person shall advertise any food, drug, cosmetic or device to the general public as a treatment, preventative or cure for any of the diseases, disorders or abnormal physical states referred to in Schedule A.1.```

could be represented as:
```{
	"actor" : {
		"value" : "person",
		"negation" : true
	},
	"actee" : {
		"value" : "general public",
		"negation" : false
	},
	"action" : {
		"value" : "advertise",
		"negation" : "true",
		"object" : ["food", "drug", "cosmetic", "device"]
	},
	"condition" : [
		{
			"actor" : {
				"value" : *for each parent NOME["action"]["object"]*,
				"negation" : false
			},
			"actee" : {
				"value" : *for each ["disease", "disorder", "abnormal physical state"]*
				"negation" : false
			},
			"action" : {
				"value" : *for each ["treat", "prevent", "cure"]*,
				"negation" : false
			}
			"condition" : null
		}
	]
}
```

