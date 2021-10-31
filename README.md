# Google-Drive-Protected-PDF-downloder
Download PDF files in case of google drive view only share or protected files share


## Follow the following steps:

- Slowly scroll down the PDF till the last
- Inspect that google drive page and go to the console option
- Past the following code to the console


```
let jspdf = document.createElement("script");
jspdf.onload = function () {
    let pdf = new jsPDF();
    let elements = document.getElementsByTagName("img");
    for (let i in elements) {
        let img = elements[i];
        console.log("add img ", img);
        if (!/^blob:/.test(img.src)) {
            console.log("invalid src");
            continue;
        }
        let can = document.createElement('canvas');
        let con = can.getContext("2d");
        can.width = img.width;
        can.height = img.height;
        con.drawImage(img, 0, 0, img.width, img.height);
        let imgData = can.toDataURL("image/jpeg", 1.0);
        pdf.addImage(imgData, 'JPEG', 0, 0);
        pdf.addPage();
    }
    pdf.save("Exported_File.pdf");
};
jspdf.src = 'https://cdnjs.cloudflare.com/ajax/libs/jspdf/1.5.3/jspdf.debug.js';
document.body.appendChild(jspdf);
```
