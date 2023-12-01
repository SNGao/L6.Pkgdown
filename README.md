# L6.Pkgdown


```{r setup, include=FALSE}
# generate the new package environment
usethis::create_package('L6.Pkgdown')

# Init the file
usethis::use_git() # init git in the local file
usethis::git_sitrep() # check status, (if link to remote website, if token available)
```

```{r}
## Link repo in the github website
# git remote add origin https://github.com/SNGao/L6.pkgdown.git
# git branch -M main
# git push -u origin main
## Use the Github Desk to upload

# Run once to configure package to use pkgdown
usethis::use_pkgdown() 

# check link condition
usethis::git_sitrep()
```

# Run to build the website

pkgdown can automatically generate a website of an R package, containing references to the enclosed function, different vignettes if exists, within two lines of code (slight exaggeration). It also helps to deploy the website to GitHub server. Amazingly, pkgdown facilitates automatic updates of the website following any changes made to the package that are pushed to GitHub.

```{r}
pkgdown::build_site()
```

If you're using GitHub, we also recommend setting up GitHub actions to automatically build and publish your site:

```{r}
usethis::use_github() # check if connect to repo already

usethis::use_pkgdown_github_pages()
```

(1)自动生成 docs/ 目录：use_pkgdown_github_pages() 将创建一个名为 docs/ 的目录，其中包含构建文档网页所需的所有文件。
(2)修改 .gitignore 文件：函数会更新 .gitignore 文件，以确保 docs/ 目录中的文件不会被 Git跟踪（.gitignore文件是网页信息的存放处，自动更新需要commit文件）。
(3)修改 .gitattributes 文件：函数还会更新 .gitattributes 文件，以确保在 Git 中正确处理二进制文件。
(4)在项目根目录创建 .nojekyll 文件：这个文件的存在告诉 GitHub Pages 不要执行 Jekyll 构建过程，因为 R 包的文档通常是用 pkgdown 构建的，而不是 Jekyll。
(5)将 gh-pages 分支推送到远程仓库：函数会创建一个名为 gh-pages的分支，并将生成的文档网页推送到 GitHub 上。

#### Install
Please intall your package, and library()

# Generate another branch to save contents in /docs file
# deploy the website from the file content and publish online.
```{r}
pkgdown::deploy_to_branch()
```

# Make website renewal based on the code
```{r}
usethis::use_github_action("pkgdown")
```
Sets up continuous integration (CI) for an R package that is developed on GitHub using GitHub Actions. CI can be used to trigger various operations for each push or pull request, e.g. running R CMD check or building and deploying a pkgdown site.

# How to use build website automatically
```{r}
## Commit files in the master and gh-page branch to the github 
## the circle on the website is the signal of deploying process
## we can click details to find more process information
```

While the pkgdown website provides a comprehensive walkthrough for those who set up their GitHub access
If you run into problem when running usethis::use_pkgdown_github_pages() and get stuck, you should try to understand what the function does by reading its manual ?usethis::use_pkgdown_github_pages().
Is it possible to create the necessary gh_pages using pkgdown::deploy_to_branch()? Don’t forget to set up the GitHub Action by calling usethis::use_github_action("pkgdown"). Now you should be able to find access your website via github_account_name.github.io/pkg_name



## Configure git with Rstudio
```{r}
## set your user name and email:
usethis::use_git_config(user.name = "YourName", user.email = "your@mail.com")

## create a personal access token for authentication:
usethis::create_github_token() 

## set personal access token:
credentials::set_github_pat("YourPAT")

## or store it manually in '.Renviron': (preferred)
usethis::edit_r_environ()
```

# Some references
Configure git with Rstudio: https://gist.github.com/Z3tt/3dab3535007acf108391649766409421
Git Guides: https://happygitwithr.com/https-pat



