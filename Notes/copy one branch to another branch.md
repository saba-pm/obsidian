```
# Clone the source repository

git clone https://gitlab.sibgmbh.com/devops/safes-chart.git

cd safes-chart

  

# Clone the destination repository in a separate directory

cd ..

git clone https://gitlab.sibgmbh.com/devops/trio-education-chart.git

cd trio-education-chart

  

# Add the source repository as a remote in the destination repository

git remote add source https://gitlab.sibgmbh.com/devops/safes-chart.git

git fetch source

  

# Ensure you are on the main branch

git checkout main

  

# Merge the school-prd branch from the source repository

git merge source/school-prd

  

# Resolve conflicts if any, commit changes

  

# Push the changes to the remote main branch

git push origin main
```