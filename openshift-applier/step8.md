Now that we see our Ruby app up and running, let's go push it up to GitHub so it can be transferred to our other cluster!

```
git init
git add README.md
git commit -m "first commit"
git remote add origin https://github.com/pcarney/applier-lab.git
```{{execute}}

Now push your work up to a branch with your name on it

```
git push -u origin <your-branch-name>
```

And now let's watch it come up in the other cluster!