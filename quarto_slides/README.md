# Quarto Slides

This directory holds the source code for the slide decks used in the Introduction to R for Clinical Data workshop, co-presented by Arcus Education and the R User Group of the Children's Hospital of Philadelphia.

These slides can be published using the `quarto publish` command, executed in the command line / terminal, *not* in the R console.  

**Tip**: Are you trying to run `quarto publish` on a CHOP-managed computer and getting authorization errors? 
Try running it on another machine; there appears to be something about how CHOP computers are set up that interferes with QuartoPub's authorization. 

## Setting up quarto to update automatically with github actions

I followed the instructions to [use GitHub Actions to automatically publish updates to QuartoPub](https://quarto.org/docs/publishing/quarto-pub.html#github-action). 
When you push changes to `main`, it will automatically trigger a workflow that should update our slide decks on QuartoPub. 

**Important**: We're not asking GitHub to actually execute all the R code (that would be very computationally expensive), so it's important that you use `quarto render` locally on your own computer after making any changes that could affect code output. 
We have [freeze computations](https://quarto.org/docs/publishing/quarto-pub.html#freezing-computations) set up in `_quarto.yml`. 
This means computations in R are done locally only, and the results are stored in `_freeze`. 
That folder needs to be version controlled so it's available on github. 
When you render, it will save the results of all the executed code in the `_freeze` directory. 
When you commit and push the changes you made to your .qmd file, be sure to add any changes to the `_freeze` directory as well. 

**Do you want to make changes to the .qmd files in this repository, and have the updates publish to QuartoPub?** 
It's all set up to work automatically! 
You should be able to just make changes, run `quarto render` in the command line from the root directory of this repo, and then commit and push your changes to the `main` branch. 
It will take several minutes, but you should see your changes reflected on QuartoPub soon.

If you want to make edits but **not** have them immediately reflected on QuartoPub, then work on a branch. 
When you merge the branch to `main`, that will trigger the action to update QuartoPub. 

**Do you want to set up a similar system in another repo?** 
You'll need to do the following: 

- You can start by copying the contents of this repository, with the exception of the `_publish.yml` file. You can't just copy the `_publish.yml` file from this repo because it's pointing to my (Rose Hartman) QuartoPub account and you won't have authorization.
- Successfully run `quarto publish` on your own computer first, to generate a `_publish.yml` file for your repo. 
- You'll need to [save a QuartoPub auth token as a secret in your repository](https://quarto.org/docs/publishing/quarto-pub.html#quarto-pub-credentials)
- Follow the rest of the instructions to [set up GitHub actions to publish to QuartoPub](https://quarto.org/docs/publishing/quarto-pub.html#github-action)

Note that this repo also has a separate actions workflow running to publish the website to GitHub Pages. You don't need to also have a GH Pages website to automatically publish to QuartoPub; those are two independent things. 

## What's in that `_quarto.yml` file?

The `_quarto.yml` file does the following:

- It tells quarto to render every .qmd file when you run `quarto render`; by default it would also attempt to render .rmd and .md files, but we don't want that since there's code in the .rmd exercises files that definitely won't work. 