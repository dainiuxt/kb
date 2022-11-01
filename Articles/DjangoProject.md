# Creating Django project and working with it

1. Create  directory and `cd` into it.

2. Make virtual `python` environment:

    ```
    python -m venv venv
    ```

    You can activate this environment every time by executing

    ```
    source venv/bin/activate
    ```

3. Install Django into virtual environment:

    ```
    pip install Django
    ```

4. Create new Django project:

    ```
    django-admin startproject yourprojectname
    ```

5. Comment `SECRET_KEY` in `settings.py` and edit it correspondingly:

    ```python
    import os

    # ...

    SECRET_KEY = os.environ.get("DJANGO_SECRET_KEY")
    ```

6. Generate `SECRET_KEY` and create `.env` file by running python command

    ```shell
    python -c 'from django.core.management.utils import get_random_secret_key; \
    print("DJANGO_SECRET_KEY="+get_random_secret_key())' > .env
    ```

7. Create `.gitignore` file with following content (more details at [djangowaves](https://djangowaves.com/tips-tricks/gitignore-for-a-django-project/)):

    ```
    # Django #
    *.log
    *.pot
    *.pyc
    __pycache__
    db.sqlite3
    media

    # Backup files # 
    *.bak 

    # If you are using PyCharm # 
    # User-specific stuff
    .idea/**/workspace.xml
    .idea/**/tasks.xml
    .idea/**/usage.statistics.xml
    .idea/**/dictionaries
    .idea/**/shelf

    # AWS User-specific
    .idea/**/aws.xml

    # Generated files
    .idea/**/contentModel.xml

    # Sensitive or high-churn files
    .idea/**/dataSources/
    .idea/**/dataSources.ids
    .idea/**/dataSources.local.xml
    .idea/**/sqlDataSources.xml
    .idea/**/dynamic.xml
    .idea/**/uiDesigner.xml
    .idea/**/dbnavigator.xml

    # Gradle
    .idea/**/gradle.xml
    .idea/**/libraries

    # File-based project format
    *.iws

    # IntelliJ
    out/

    # JIRA plugin
    atlassian-ide-plugin.xml

    # Python # 
    *.py[cod] 
    *$py.class 

    # Distribution / packaging 
    .Python build/ 
    develop-eggs/ 
    dist/ 
    downloads/ 
    eggs/ 
    .eggs/ 
    lib/ 
    lib64/ 
    parts/ 
    sdist/ 
    var/ 
    wheels/ 
    *.egg-info/ 
    .installed.cfg 
    *.egg 
    *.manifest 
    *.spec 

    # Installer logs 
    pip-log.txt 
    pip-delete-this-directory.txt 

    # Unit test / coverage reports 
    htmlcov/ 
    .tox/ 
    .coverage 
    .coverage.* 
    .cache 
    .pytest_cache/ 
    nosetests.xml 
    coverage.xml 
    *.cover 
    .hypothesis/ 

    # Jupyter Notebook 
    .ipynb_checkpoints 

    # pyenv 
    .python-version 

    # celery 
    celerybeat-schedule.* 

    # SageMath parsed files 
    *.sage.py 

    # Environments 
    .env 
    .venv 
    env/ 
    venv/ 
    ENV/ 
    env.bak/ 
    venv.bak/ 

    # mkdocs documentation 
    /site 

    # mypy 
    .mypy_cache/ 

    # Sublime Text # 
    *.tmlanguage.cache 
    *.tmPreferences.cache 
    *.stTheme.cache 
    *.sublime-workspace 
    *.sublime-project 

    # sftp configuration file 
    sftp-config.json 

    # Package control specific files Package 
    Control.last-run 
    Control.ca-list 
    Control.ca-bundle 
    Control.system-ca-bundle 
    GitHub.sublime-settings 

    # Visual Studio Code # 
    .vscode/* 
    !.vscode/settings.json 
    !.vscode/tasks.json 
    !.vscode/launch.json 
    !.vscode/extensions.json 
    .history
    ```

