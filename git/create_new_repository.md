# Create a new repository locally and connect to remote 

* Initialize the local directory as a Git repository.

  ```git init```

* Add the files in your new local repository. This stages them for the first commit.

  ```git add --all```

* Commit the files that you’ve staged in your local repository.

  ```git commit -m "initial commit```

* Copy the https url of your newly created repo. In the Command prompt, add the URL for the remote repository where your local repository will be pushed.

  ``` git remote add origin remote repository URL```

  ```git remote -v```

* Push the changes in your local repository to GitHub.

  ```git push -f origin master```
