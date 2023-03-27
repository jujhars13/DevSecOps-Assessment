# Software Delivery Discussion Cards

Temporarily published to [https://wayne-tw.github.io/engineering-capability-assessment-cards/](https://wayne-tw.github.io/engineering-capability-assessment-cards/)

Cards used to assess the DevSecOps capability of a team.

Inspired by the physical [software delivery cards](https://agilestationery.com/products/software-delivery-assessment-card-deck-by-matthew-skelton) from [Matthew Skelton](https://uk.linkedin.com/in/matthewskelton)

Use these cards to assess the DevSecOps capability of a team which you can then plot on the [DevSecOps capability model](https://devsecops.jujhar.com/).

## Local Dev

```bash
# OPTIONAL use the awesome `reload` which auto-refreshes your browser on change using websockets
# `npm install -g webpack webpack-cli reload`

# install dev and app deps
npm install

# in the root of the repo
node_modules/.bin/webpack --watch
(cd docs && reload -e "html|js|css|json|yml")

# browse to http://localhost:8080/
```

## Pushing to prod

Published via Github pages atm, so build to `docs` using `webpack` and just push to `main` to publish.

Temporarily published to [https://jujhars13.github.io/devsecops-assessment-cards/](https://jujhars13.github.io/devsecops-assessment-cards/)

```bash
# simply build for prod
NODE_ENV=production node_modules/.bin/webpack build
# now git commit and push to main
```

## The dataset as CSV to JSON

We find working with CSVs the most straightforward using a standard spreadsheet app.
You can then produce the other formats we need (`jsonl` -> `json`) using Python [`csvkit`](https://csvkit.readthedocs.io/en/latest/tutorial.html) and then [`jq`](https://stedolan.github.io/jq/) to spit out a denormalised json array that's easier to digest by our client-side js:

```bash
# use Python csvjson from csvkit to convert our csv file to a jsonl then to a json file
# pip3 install csvkit
csvjson questions/dev-assessment-cannonical.csv | jq -c '.[]' > /tmp/data.jsonl
jq -s '.' /tmp/data.jsonl > src/js/cardData.json

# as one line
# To generate questions set from CSV to json
$(csvjson questions/dev-assessment-cannonical.csv | jq -c '.[]' | jq -s '.' > src/js/cardData.json)

# To generate moreCardInfo from CSV to json
$(csvjson moreCardInfo.csv | jq -c '.[]' | jq -s '.' > src/js/moreCardInfo.json)
```

## TODO

- [x] fix more-info accordian style
- [x] create CSV file for more-info data
- [x] update readme with instructions for generating more-info json
- [x] populate csv with more-info data

## Licence

Fill your boots

[MIT](LICENSE)
