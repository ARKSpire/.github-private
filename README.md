<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Shipping Documentation</title>
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: #E3F2FD;
            color: #0D47A1;
            margin: 0;
            padding: 20px;
            display: flex;
            flex-direction: column;
            align-items: center;
        }

        h1 {
            font-size: 2.5rem;
            margin-bottom: 20px;
        }

        h2 {
            font-size: 1.8rem;
            margin: 20px 0;
        }

        form, table {
            width: 90%;
            max-width: 800px;
            margin: 0 auto;
            background: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        }

        form div {
            margin-bottom: 15px;
        }

        label {
            display: block;
            margin-bottom: 5px;
            font-weight: bold;
        }

        input, select, button {
            width: 100%;
            padding: 10px;
            font-size: 1rem;
            border: 2px solid #0288D1;
            border-radius: 5px;
            outline: none;
        }

        input[type="file"] {
            padding: 5px;
        }

        button {
            background-color: #0288D1;
            color: white;
            cursor: pointer;
            transition: background-color 0.3s ease, transform 0.2s;
        }

        button:hover {
            background-color: #01579B;
        }

        button:active {
            transform: scale(0.98);
        }

        table {
            width: 100%;
            border-collapse: collapse;
            margin: 20px 0;
        }

        th, td {
            border: 1px solid #ddd;
            padding: 10px;
            text-align: left;
        }

        th {
            background-color: #f2f2f2;
        }

        td button {
            margin-right: 5px;
            width: auto;
        }

        #statusMessage {
            margin-top: 15px;
            font-size: 1rem;
            color: green;
        }
    </style>
</head>
<body>
    <header>
        <h1>Shipping Documentation</h1>
    </header>
    
    <div>
        <h2>Upload New Document</h2>
        <form id="upload-form">
            <div>
                <label for="doc-title">Document Title:</label>
                <input type="text" id="doc-title" name="doc-title" placeholder="Enter document title" required>
            </div>
            <div>
                <label for="doc-type">Document Type:</label>
                <select id="doc-type" name="doc-type">
                    <option value="contract">Contract</option>
                    <option value="invoice">Invoice</option>
                    <option value="compliance">Compliance Certificate</option>
                </select>
            </div>
            <div>
                <label for="doc-file">Upload File:</label>
                <input type="file" id="doc-file" name="doc-file" required>
            </div>
            <div>
                <button type="button" id="upload-btn">Upload Document</button>
            </div>
        </form>

        <h2>Document List</h2>
        <table>
            <thead>
                <tr>
                    <th>Title</th>
                    <th>Type</th>
                    <th>Date Uploaded</th>
                    <th>Actions</th>
                </tr>
            </thead>
            <tbody id="document-list">               
                <!-- Document rows will be dynamically added here -->
            </tbody>
        </table>
    </div>

    <script>
        const uploadBtn = document.getElementById('upload-btn');
        const documentList = document.getElementById('document-list');

        uploadBtn.addEventListener('click', () => {
            const title = document.getElementById('doc-title').value;
            const type = document.getElementById('doc-type').value;
            const fileInput = document.getElementById('doc-file');

            if (!title || !fileInput.files.length) {
                alert("Please fill all fields and select a file.");
                return;
            }

            const file = fileInput.files[0];
            const date = new Date().toISOString().split('T')[0]; 

            const newRow = document.createElement('tr');
            newRow.innerHTML = `
                <td>${title}</td>
                <td>${type}</td>
                <td>${date}</td>
                <td>
                    <button class="view-btn">View</button>
                    <button class="delete-btn">Delete</button>
                </td>
            `;
            documentList.appendChild(newRow);

            const viewBtn = newRow.querySelector('.view-btn');
            const deleteBtn = newRow.querySelector('.delete-btn');

            // Simulate file viewing
            viewBtn.addEventListener('click', () => {
                const fileURL = URL.createObjectURL(file);
                window.open(fileURL, '_blank');
            });

            // Remove the row on delete
            deleteBtn.addEventListener('click', () => {
                documentList.removeChild(newRow);
            });

            // Reset the form
            document.getElementById('upload-form').reset();
        });
    </script>
</body>
</html>
