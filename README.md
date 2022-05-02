# Quantium starter repo

blah blah blah
</br></br>
<b>Task 1:</b> Set Up Your Local Development Environment

* Clone the quantium-starter-repo repository using this command:
<pre>
git clone https://github.com/vagabond-systems/quantium-starter-repo.git
</pre>
* Download and install Pycharm Community Edition using this link: https://www.jetbrains.com/pycharm/download/#section=windows
* Create a new virtual environment
<pre>
python -m venv quantium
</pre>
* Activate your virtual environment
<pre>
.\quantium\Scripts\activate # Windows 
</pre>
* Install dependencies and add a virtual environment to the Python Kernel
python -m pip install --upgrade pip
pip install ipykernel
python -m ipykernel install --user --name=quantiumj
* Add the dash and pandas packages as dependencies to your virtual environment
<pre>
pip install dash
pip install pandas
</pre>
* To check your installed dependencies using this command: 
<pre>
pip list
</pre>
* With your virtual environment active, install all the necessary dash testing dependencies
<pre>
pip install dash[testing]
</pre>
* Commit your changes and push them to GitHub. To add a large library in git, first download Git Large File Storage (LFS) using this link: https://git-lfs.github.com/
* Then compressed the library folder in a zip folder. Go to the command prompt and run these command: 
<pre>
git lfs install
git lfs track "*.zip" #format of the file or folder
git add .gitattributes
git add filename.zip
git commit -m "Add Zip File"
git push origin main
</pre>
* Submit a link to your repo in the right module.
