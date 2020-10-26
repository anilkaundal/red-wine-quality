# Red Wine Quality :wine_glass:
This is an experimental repository to try out one of the most powerful ideas from the DevOps revolution, 
continuous integration in data science/machine learning project. Here I have created an automatic model 
training & testing setup using [GitHub Actions](https://github.com/features/actions) and [Continuous Machine Learning](https://github.com/iterative/cml) (CML)
[two free and open-source tools in the Git ecosystem]. I have used CML for comparing 
ML experiment across it's project history. In this experiment, I'm modelling a [kaggle dataset](https://www.kaggle.com/uciml/red-wine-quality-cortez-et-al-2009) of red wine properties and quality ratings.

*The key file in any CML project is .github/workflows/cml.yaml.*

#### Here is an example template for creating a cml.yaml file.
```
name: your-workflow-name
on: [push]
jobs:
  run:
    runs-on: [ubuntu-latest]
    container: docker://dvcorg/cml-py3:latest
    steps:
      - uses: actions/checkout@v2
      - name: cml_run
        env:
          repo_token: ${{ secrets.GITHUB_TOKEN }}
        run: |

          # Your ML workflow goes here
          pip install -r requirements.txt
          python train.py

          # Write your CML report
          cat results.txt >> report.md
          cml-send-comment report.md
```
