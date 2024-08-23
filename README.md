# HCI ISP Checksum Calculator

This is a brute-force algorithm that discovers the checksum calculation method used for HCI ISP. It analyzes
identification numbers with a checksum character at the end, computes
possible weights for each digit, and verifies the consistency of the checksum calculation.

The list of identification numbers is obtained from [ISP Pick Students](https://isp.hci.edu.sg/pickStudents2.asp) by
running the following javascript code:

```js
console.log(Array.from(new Set(Array.from(document.querySelectorAll('.normal'))
    .map(e => e.innerText.slice(0, 7)))).join('\n'));
```

Eventually, the weights and mapper are found and they are given below:

```python
weights = [0, 1, 3, 1, 2, 7]
mapping = {11: 'A', 12: 'B', 10: 'E', 9: 'H', 8: 'J', 7: 'L',
           6: 'M', 5: 'N', 4: 'R', 3: 'U', 2: 'W', 1: 'X', 0: 'Y'}
```

By inspection, the identification numbers are distributed in order of different groups of students, and within each
group, they are sorted by
name. On the right, the numbers show the boundary numbers for the batch of 2020:

| Group       | Start  | End    |
|-------------|--------|--------|
| Scholars    | 202157 | 202173 |
| High School | 202174 | 202555 |
| NYGH        | 202556 | 202945 |
| JAE         | 202946 | 203251 |

This set of numbers would in theory mean that there are 1095 in the cohort. However, in reality there are only 1057
students. This is due to some numbers not being taken, presumably due to errors in the admission process.

It is also interesting to note that the 2020 batch started from an identification number of xx2157, but previous batches
began counting from a much lower number of below xx1600.