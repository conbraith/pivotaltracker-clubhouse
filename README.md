# pivotaltracker-clubhouse

Simple tool to transfer stories from Pivotal Tracker to Clubhouse.

## Python Package Dependencies

I use `pip` and `pipenv` to manage dependencies, etc. If you're on MacOS I'd recommend using `brew` to install `pipenv`.

Installing dependencies:

```
pipenv install
```

Running script:

```
pipenv run python ./pivotaltracker-clubhouse --ptoken "<pivotal_token>" --ctoken "<clubhouse_token>" --pproject "<pivotal_project_id>" --cproject "<clubhouse_project_id>"
```

## Usage

```
usage: pivotaltracker-clubhouse [-h] --ptoken PTOKEN --ctoken CTOKEN
                                --pproject PPROJECT --cproject CPROJECT

optional arguments:
  -h, --help           show this help message and exit

required arguments:
  --ptoken PTOKEN      The app token of the Pivotal Tracker user. See
                       https://www.pivotaltracker.com/help/articles/api_token/
  --ctoken CTOKEN      An app token of the Clubhouse user. See
                       https://clubhouse.io/api/v1/#authentication
  --pproject PPROJECT  The Pivotal Tracker project ID from which to transfer
                       stories.
  --cproject CPROJECT  The Clubhouse project ID to which to transfer stories.
  --dry-run True       Dry run
  --default-user ID    Default user to associate stories to if none is found
  --skip-duplicates    Skip stories already imported
```

## API Token Retrieval Instructions

- https://www.pivotaltracker.com/help/articles/api_token/
- https://clubhouse.io/api/v1/#authentication

## Notes

Not all information is preserved. See the code for precise details.

You can adjust what's pulled from Pivotal by changing `pquery` in the `_run`
method. It just hits the Pivotal API, so you have lots of options. By default,
it pulls all features, chores and bugs.

This will import stories and comments and associate both to users. If a user
doesn't have a Clubhouse account, it will use the default user ID specified
when running the command.

If you run the tool multiple times, you will have duplicate stories unless
you use the `skip-duplicates` features. Obviously enough, if you change
the implementation, you'll need to re-address how you proceed.

An additional label "pivotal" is attached to each imported story,
and the Clubhouse story `external_id` is set to the ID of the Pivotal story.

Stories in Pivotal are preserved, not deleted.

## State-mapping

- Retrieve workflow from Clubhouse: https://api.clubhouse.io/api/v2/workflows
- Update `state-mapping.json` (see `state-mapping.json.example`)
