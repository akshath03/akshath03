Creating a new Assignment
=========================

Assignment Setup
----------------

- Enter Assignment Name
- Add Part
	- Click Part -> Enter Part Name
	- Lab Type -> Jupyter Notebook
	- Submission -> Set Due Date
- Options -> Enable Team Project
- Click Save 

Jupyter Notebook Setup
----------------------

- Configure Workspace
- Jupyter -> Launch Jupyter Server
- Upload the Jupyter Notebook
- Teacher View
	- Check for nbgrader Markdown, Solution and auto-grader tab assigned properly.
	- Check for correct points allocated for each question in the auto-grader tab.
- Student View
	- Check if solution or the hidden tests are visible.
	- Check for clarity of images and texts.
- Update
- Jupyter -> Release Notebook(s)
- Under the Assignment Setup tab -> Publish

Create a Homework link in Brightspace after the assignment is published in Vocareum.

Plagiarism Check
----------------

- Configure Workspace
- Open in Standard view (View -> Standard)
- Choose the grade.sh file (resource -> scripts -> grade.sh)
- Update the grade.sh code

.. code:: python

vocJupyterGradeNotebookWithTraceback hw00.ipynb

python << EOF
import nbformat

filename = "hw00.ipynb"
nb = nbformat.read(filename, as_version=nbformat.NO_CONVERT)
starter_code_nb = nbformat.read("../resource/startercode/" + filename,as_version=nbformat.NO_CONVERT)

code_input = ""
for cell in nb['cells']:
    if 'nbgrader' in cell['metadata'].keys():
        if cell['metadata']['nbgrader']['solution'] == True:
            code_input += cell['source']
            code_input += "\n"

starter_code = ""
for cell in starter_code_nb['cells']:
    if 'nbgrader' in cell['metadata'].keys():
        if cell['metadata']['nbgrader']['solution'] == True:
            starter_code += cell['source']
            starter_code += "\n"

code_input_lines =  code_input.split("\n")
starter_code_lines = starter_code.split("\n")

student_input_lines = [l for l in code_input_lines if not l in starter_code_lines]

with open("student_input.py", "w") as f:
    f.write("\n".join(student_input_lines))
EOF
vocSaveExecutionDataPublic student_input.py

- Assignment Setup Page
- Go to Dashboard
- Controls -> Reset autograde flags -> Auto-grade
- Go to Plagiarism tab
- Enter the extension '.py'
- Start Analysis
- Check the report 