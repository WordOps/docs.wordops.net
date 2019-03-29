# WordOps Documentation

## Contributing

Anyone can contribute and improve WordOps documentation. Pull requests are warmly welcome.

### How to contribute

#### Edit page content directly from Github

Browse the documentation and use the edit button available on the top right to open the file with Github editor

![edit](https://img.virtubox.net/images/2019/03/29/image.png)

You can edit content directly from Github by browsing the folder docs and by using the button "edit this file" available on the right.
Github will automatically fork the repository (copy the repository in your account) and after you finished making changes, you will be able to commit changes (saving changes with a message which describe what was added/changed/removed).
The last step to apply changes on this repository is to open a PR(pull request). We will review the commits you made and if everything is okay, we will merge the PR.

#### Work on the documentation locally

WordOps documentation is built with [mkdocs](https://github.com/mkdocs/mkdocs) and [mkdocs-material](https://github.com/squidfunk/mkdocs-material).

Mkdocs provide the ability to write documentation content in markdown, and to generate and publish static html files on github pages service.

If you want to work on WordOps documentation on your computer, you just have to :

- clone the repository `git clone https://github.com/WordOps/docs.wordops.io.git`
- install mkdocs : [guide for windows](https://gist.github.com/VirtuBox/2f149ce45e2449c36f18cb634243fe90)
- edit the documentation with live preview by running the command `mkdocs serve` or `mkdocs.exe serve` inside the repository folder
This will display the documentation on http://127.0.0.1:8000
