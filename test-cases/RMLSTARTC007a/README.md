## RMLSTARTC007a

**Title**: non-asserted quoted triples in subject and object, one source

**Description**: Tests the creation of a two non-asserted quoted triples, one in the position of subject and other in object with data from one file

**Error expected?** No

**Input**
```
c1,c2,c3,c4
s1,o1,s2,o2
```

**Mapping**
```
@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
@prefix rml: <http://w3id.org/rml/> .
@prefix ex: <http://example/> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .
@prefix : <http://example.org/> .
@base <http://example.org/> .

:firstTM a rml:NonAssertedTriplesMap ;
    rml:logicalSource [
        rml:source [ a rml:Source, rml:RelativePathSource;
            rml:path "data.csv";
        ];
        rml:referenceFormulation rml:CSV
    ];
    rml:subjectMap [
        rml:template "http://example/{c1}"
    ];
    rml:predicateObjectMap [
        rml:predicate ex:p1 ;
        rml:objectMap [
            rml:template "http://example/{c2}"
        ]
    ] .

:secondTM a rml:AssertedTriplesMap ;
    rml:logicalSource [
        rml:source [ a rml:Source, rml:RelativePathSource;
            rml:path "data.csv";
        ];
        rml:referenceFormulation rml:CSV
    ];
    rml:subjectMap [
            rml:quotedTriplesMap :firstTM
    ];
    rml:predicateObjectMap [
        rml:predicate ex:q; ;
        rml:objectMap [
            rml:quotedTriplesMap :thirdTM
        ]
    ] .

:thirdTM a rml:NonAssertedTriplesMap ;
    rml:logicalSource [
        rml:source [ a rml:Source, rml:RelativePathSource;
            rml:path "data.csv";
        ];
        rml:referenceFormulation rml:CSV
    ];
    rml:subjectMap [
        rml:template "http://example/{c3}"
    ];
    rml:predicateObjectMap [
        rml:predicate ex:p2 ;
        rml:objectMap [
            rml:template "http://example/{c4}"
        ]
    ] .

```

**Output**
```
<< <http://example/s1> <http://example/p1> <http://example/o1> >> <http://example/q> << <http://example/s2> <http://example/p2> <http://example/o2> >> .

```

