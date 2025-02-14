# Instant Articles

**If you are seeking package for generating instant article or feeds in Masonite then yes, this package is for you.**

> This helps you generate facebooks instant articles and also regular feeds with enough customizations you might need.

### How to?

##### Step 1: Install package

Install package by executing the following command.

```shell
pip install masonite-instant-article
```

##### Step 2: Publish Resource Files

You need to have some files setup and don't worry it's quite easy. You just have to execute the following command.

```shell
python craft instant_article
```

##### Step 3: Update Configurations

You need to define options in your `instant_article` configuration file inside `config` directory.

```python
# config
INSTANT_ARTICLE = {
    "force_validate": False,
    "feed_details": {
        "your-custom-route-name.xml": {
            'model': 'path-to-your-model-class',
            'title': '',
            'description': '',
            'lang': 'en-us',
            'brand': '',
            'type': 'instant-article' # feed, instant-article
        }
    }
}

# Example
INSTANT_ARTICLE = {
    "force_validate": False,
    "feed_details": {
        "blogs-rss.xml": {
            'model': 'app.models.Blog',
            'title': 'Blog Feed',
            'description': '',
            'lang': 'en-us',
            'brand': '',
            'type': 'instant-article' # feed, instant-article
        },
        "news-rss.xml": {
            'model': 'app.models.News',
            'title': 'News Feed',
            'description': '',
            'lang': 'en-us',
            'brand': '',
            'type': 'instant-article' # feed, instant-article
        }
    }
}

# Above feeds can be access from:
"""
https://your-domain.com/rss/blogs-rss.xml
https://your-domain.com/rss/news-rss.xml
"""
```

#### Step 4: Implement Instant Article Interface to your Model and configure as follows

```python
from instant_article.interfaces.instant_article_interface import InstantArticleInterface
from instant_article.models.instant_article import InstantArticle


class YourModel(Model, InstantArticleInterface):


    @staticmethod
    def get_feed_items():
        return YourModel.all() # can be any query returning proper values

    def format_feed(self):
        return InstantArticle.create({
            'id': self.id, # required | integer
            'title': self.name, # required | string
            'subtitle': '', # nullable | string
            'kicker': '', # nullable | string
            'summary': '', # required | string
            'description': '', # required | string
            'cover': '', # nullable | string
            'updated': self.updated_at, # required | date
            'published': self.created_at, # required | date
            'link': '', # full url to item...
            'author': '' # nullable | email | string
        })
```

##### Step 5: Awesome

1. Your project is now ready to go :+1:.
