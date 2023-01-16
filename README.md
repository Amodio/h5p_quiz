# h5p_quiz
Get the questions/answers from a H5P quiz.

## How?
Copy/paste this into your console (F12) from (for example) [module1 eval](https://www.drsd.defense.gouv.fr/lhabilitation-secret-defense-quizz-n1-3) or [module2 eval](https://www.drsd.defense.gouv.fr/les-informations-et-supports-classifies-quizz-n2-1) :
```
var myWindow = window.open("", "", "width=800,height=600");
for (const question of JSON.parse(H5PIntegration.contents[Object.keys(H5PIntegration.contents)].jsonContent).questions) {
    myWindow.document.write('Q: ' + question.params.question.trim() + '<br />\n');
    for (const answer of question.params.answers) {
        if (answer.correct == true) {
            myWindow.document.write('A: ' + answer.text.trim() + '<br />\n<br />\n');
        }
    }
}
```

## Notes
We could print directly the two required codes as they are transmitted in plaintext (tests in javascript, client side).

Now.. this website generates a PDF via "dompdf 1.0.2 + CPDF". This package was released two years ago (the 8th of January, in 2021) and a few critical CVE are public:
* https://github.com/dompdf/dompdf/wiki/Securing-dompdf#previously-disclosed-vulnerabilities
* https://positive.security/blog/dompdf-rce
* https://tantosec.com/blog/cve-2022-41343/
* https://huntr.dev/bounties/0bdddc12-ff67-4815-ab9f-6011a974f48e/
* https://huntr.dev/bounties/a6071c07-806f-429a-8656-a4742e4191b1/
* https://huntr.dev/bounties/73dbcc78-5ba9-492f-9133-13bbc9f31236/
* https://huntr.dev/bounties/a6da5e5e-86be-499a-a3c3-2950f749202a/
* https://github.com/dompdf/dompdf/releases

## Disclaimer
The contents of this document are provided for general information only, do not try to exploit anything but your own machine.
