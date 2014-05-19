## Patterns

It is possible to create annotations based on sequence patterns.
The command [find_pattern](http://deepblue.mpi-inf.mpg.de/api.html#api-find_pattern) creates an annotation based on the given pattern. This command has 3 parameters: The pattern, in [Perl Regular Expression Syntax](http://www.boost.org/doc/libs/1_44_0/libs/regex/doc/html/boost_regex/syntax/perl_syntax.html), the ```genome``` and a boolean, to specify if the pattern matching will be overlapping or non-overlapping.

The difference between overlapping and non-overlapping is: In overlapping, when the pattern is found, the pattern searching continues in the position after the pattern found. In the overlapping, the searching process start one position after the beginning of the match.

```
status, _id = server.find_pattern("TATA", "hg19_only_chr19", True, user_key)
print server.info(_id, user_key)
```

### Patterns Metafield

It is possible to get the number of times that a pattern happens with the Metafilds: ```@COUNT.NON-OVERLAP(PATTERN)``` and ```@COUNT.NON-OVERLAP(PATTERN)``


```python
(status, _id) = server.find_pattern("CG", "hg19", False, user_key)
(status, _id) = server.find_pattern("TATA", "hg19", False, user_key)
(status, _id) = server.find_pattern("(TATA|CG)", "hg19", False, user_key)

(status, ann) = server.select_annotations("CpG Islands", "hg19", "chr1", 1, 500000, user_key)
   
fmt = "CHROMOSOME,START,END,@NAME:none,@LENGTH,@COUNT.NON-OVERLAP(TATA),@COUNT.NON-OVERLAP(CG),@COUNT.NON-OVERLAP((TATA|CG))"
(status, regions) = server.get_regions(ann, fmt, user_key)
```