<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Student Result Search</title>
    <script src="https://mozilla.github.io/pdf.js/build/pdf.js"></script>
</head>
<body>
    <h1>Search Student Result</h1>
    <input type="text" id="studentNumber" placeholder="Enter Student Number">
    <button onclick="searchResult()">Search</button>
    <div id="result"></div>

    <script>
        function searchResult() {
            const studentNumber = document.getElementById('studentNumber').value;
            const pdfUrl = '[LINK_TO_YOUR_PDF_FILE](https://drive.google.com/drive/folders/13X7S3_R0ZrHAdNfns2gQCwJz4i4fsAbh?usp=sharing)'; // استبدل هذا بالرابط المباشر لملف PDF الخاص بك
            const loadingTask = pdfjsLib.getDocument(pdfUrl);

            loadingTask.promise.then(pdf => {
                pdf.getPage(1).then(page => {
                    page.getTextContent().then(textContent => {
                        const text = textContent.items.map(item => item.str).join(' ');
                        if (text.includes(studentNumber)) {
                            document.getElementById('result').innerText = Result found for student number ${studentNumber};
                        } else {
                            document.getElementById('result').innerText = 'Student number not found';
                        }
                    });
                });
            }).catch(error => {
                console.error('Error fetching the PDF file:', error);
            });
        }
    </script>
</body>
</html>
