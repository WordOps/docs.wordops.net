# WordOps Documentation

WordOps documentation sources files are stored in this repository.

## Contributing

Anyone can contribute and improve WordOps documentation. Pull requests are warmly welcome.

You can either edit page content from Github or fork the repository before cloning it on your computer to work with the text editor of your choice.

If you have any question about this documentation, feel free to join us on [Slack](https://community.wordops.io/slack) or to ask your question on [WordOps Community forum](https://community.wordops.net/)

### Method 1 : Edit page content directly from Github

![edit](https://img.virtubox.net/images/2019/03/29/image.png)

1. Browse the documentation and use the edit button available on the top right to open the file with Github editor
2. Edit content directly from Github by browsing the folder docs and by using the button "edit this file" available on the right.
3. Github will automatically fork the repository (copy the repository in your account)
4. After you finished making changes, you will be able to commit changes (saving changes with a message which describe what was added/changed/removed).
5. The last step to apply changes on this repository is to open a PR(pull request). We will review the commits you made and if everything is okay, we will merge the PR.

### Method 2 : Work on the documentation locally

If you want to work on WordOps documentation on your computer, you just have to :

1. Fork the repository using the button "Fork" available on the top right of this page
2. clone the forked repository :

    - with the CLI : `git clone https://github.com/YourUsername/docs.wordops.net.git`
    - or using [Github Desktop App](https://desktop.github.com/)

3. create/edit markdown files
4. commit your modification `git add . && git commit -am "your commit message"`
5. push your modification `git push`
6. open a pull request

### Working with mkdocs

WordOps documentation is built with [mkdocs](https://github.com/mkdocs/mkdocs) and [mkdocs-material](https://github.com/squidfunk/mkdocs-material).

Mkdocs provide the ability to build a static documentation site, with source files written in Markdown, and configured with a single YAML configuration file.
MkDocs builds completely static HTML sites that you can host on GitHub page or anywhere else.

You can install Mkdocs locally to use the site live preview feature.

- install mkdocs :
  - [guide for windows](https://gist.github.com/VirtuBox/2f149ce45e2449c36f18cb634243fe90)
  - `apt install mkdocs -y` on debian/ubuntu
- start mkdocs built-in web-server  `mkdocs serve` or `mkdocs.exe serve` inside the repository folder
- browse documentation live preview on http://127.0.0.1:8000

You can learn more about mkdocs usage on the [official documentation](https://www.mkdocs.org/user-guide/writing-your-docs/)