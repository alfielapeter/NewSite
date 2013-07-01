OS Malaria
==========

Background
----------

The opensourcemalaria.org website actually consists of two separate code bases.

### Website Code Base ###

There is a website code base at the Github account/repository https://github.com/OpenSourceMalaria/OSM_Website_Code.
This repository holds the HTML, CSS, images, and javascript of the website.

### osm-feeds Coed Base ###

There is a separate code base stored on heroku.com. This repository creates a simple server application
(called osm-feeds) that runs on the heroku platform. The server application is an intermediary between the code running
on the (potentially) many browsers that can be running the website code at the same time.

osm-feeds gets requests from a browser to return one of three things, or to reset its cache.

##### The things that can be returned from osm-feeds are: #####

#### The latest twitter feed for Open Source Malaria. ####
The osm-feeds application authenticates itself to Twitter (requirement of twitter). Since the authentication
requires secret information, this application ensures that the secret information remains secret!

#### The latest Project activity (from the OpenSourceMalaria github account) ####
The osm-feeds application authenticates itself to github to avoid rate limiting on requests per hour. Since the authentication
requires secret information, this application ensures that the secret information remains secret! The application also
caches the information so that requests to github do not occur excessively if there are many users viewing the site
at the same time.

#### The current list of sponsors and members from the OpenSourceMalaria github account) ####
The osm-feeds application authenticates itself to github to avoid rate limiting on requests per hour. Since the authentication
requires secret information, this application ensures that the secret information remains secret!

#### Reset command ####

The reset command is invoked to discard the contents of the cache and force the application to get and return
the current project activity data from github the next time a request for that data is made.


Content Management Solution
---------------------------

The lists of team members and sponsors are maintained on GitHub, in a public repository.

The repository is : https://github.com/OpenSourceMalaria/OSM_Website_Data/issues

There are two items in the issues list. They are "team" and "sponsors".

Team
----

  The body of the "team" issue contains a JSON array, as follows:

      [
        { "name": "Tim Connor", "affiliation": "El Hefe", "url": "www.cloudcity.io" },
        { "name": "Mat Todd",
          "affiliation": "University of Sydney",
          "url": "groups.chem.usyd.edu.au/todd/the-boss.html",
          "gravatar_email": "},
        { "name": "Stephanie Geerlings" }
      ]

  The elements: url, affiliation, and gravatar_email are optional. If name is not provided, "Anonymous" is used for their name.

  The different display cases are:

   If name, affiliation, and url provided: "Member Name, letters" as a link to the url.
   If name, url provided: "Member Name" as a link to the url.
   If name, affiliation provided: "Member Name, affiliation" without a link.
   If gravatar_email provided, the member's gravatar is obtained and shown. If missing, a default image is shown.

Sponsors
--------

  The body of the "sponsors" issue contains a JSON array, as follows:

  [
    {"name": "University of Sydney",
     "url": "sydney.edu.au",
    "image": "f.cloud.github.com/assets/1546321/620163/037d300e-cede-11e2-8e2f-e2dd51ab963c.png"
    },
    { "name": "Medicines for Malaria Venture",
    "url": "www.mmv.org",
    "image": "f.cloud.github.com/assets/1546321/620180/651b7438-cede-11e2-8706-c56f89b70947.jpg"
    },
    {"name": "Australian Research Council",
    "url": "arc.gov.au",
    "image": "f.cloud.github.com/assets/1546321/620173/2663fc4c-cede-11e2-8725-753d3de70430.jpg"
    },
    { "name": "Cloud City Development",
    "url": "cloudcity.io",
    "image": "f.cloud.github.com/assets/1546321/621382/facee53c-cf01-11e2-9456-01eee6ca7577.png"
    }
  ]

    The name and url elements are optional.

    If the name element is omitted, it defaults to the url text, if that is provided.
    If the url element is not specified for a sponsor, only the image is displayed for that sponsor.
    If all three elements are specified for a sponsor, the image is displayed and is a link to the sponsor's url,
    and the hover text is the sponsor name.