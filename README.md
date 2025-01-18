# .github-private
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width,initial-scale=1.0">
    <title>Shipping Documentation</title>
    <style>
        table {
            width: 100%;
            border-collapse: collapse;
            margin: 20px 0;
        }
        th, td {
            border: 1px solid #ddd;
            padding: 8px;
            text-align: left;
        }
        th {
            background-color: #f2f2f2;
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
                <tr>
                    <td>Shipping Letter of Instruction</td>
                    <td>Invoice</td>
                    <td>2025-01-17</td>
                    <td><button class="view-btn">View</button> <button class="delete-btn">Delete</button></td>
                </tr>
                <tr>
                    <td>Credit Application Form</td>
                    <td>Invoice</td>
                    <td>2025-01-17</td>
                    <td><button class="view-btn">View</button> <button class="delete-btn">Delete</button></td>
                </tr>
                <tr>
                    <td>Power of Attorney</td>
                    <td>Contract</td>
                    <td>2025-01-17</td>
                    <td><button class="view-btn">View</button> <button class="delete-btn">Delete</button></td>
                </tr>
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
            document.getElementById('upload-form').reset;
            const deleteBtn = newRow.querySelector('.delete-btn');
            deleteBtn.addEventListener('click', () => {
                documentList.removeChild(newRow);
            });
        });
        const deleteButtons = document.querySelectorAll('.delete-btn');
        deleteButtons.forEach((btn) => {
            btn.addEventListener('click', (event) => {
                const row = event.target.closest('tr');
                documentList.removeChild(row);
            });
        });
    </script>
</body>
</html>

