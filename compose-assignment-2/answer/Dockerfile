FROM drupal:8.6

# install -y means automatically say yes, it won't prompt to install git
# every time we use apt-get update, it uses cache so we want to delete that cache which is at least 10 MB
# / means include the next line in this command && means if the first command succeeds then use the next one
RUN apt-get update && apt-get install -y git \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /var/www/html/themes

# only download this particular branch and the latest copy, we dont need the whole history of commits only latest commits
# all the commands here are gonna run as root so these files are downloaded 
# and put in that directory as root but the apache web server expects these files to be www-data user
# we change the ownership to user:group as chown -R www-data:www-data 
# https://www.oreilly.com/library/view/enterprise-mac-security/9781430227304/9781430227304_using_chown_and_chmod_to_manage_permissi.html
RUN git clone --branch 8.x-3.x --single-branch --depth 1 https://git.drupal.org/project/bootstrap.git \
    && chown -R www-data:www-data bootstrap

WORKDIR /var/www/html

