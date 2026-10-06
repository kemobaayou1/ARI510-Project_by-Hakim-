# Retail Trader Intent Classification Dataset
#data link 
https://drive.google.com/file/d/1hDKKf2OuXPnUgJwmlkCNlsTumzJumZA8/view?usp=sharing
## Project Overview

This project creates a human-annotated dataset for identifying trading intentions in finance-related Reddit posts. For each post, annotators choose one of four labels:

1. Buy / Increase
2. Sell / Decrease / Short
3. Hold
4. No Clear Trade Intent

The goal is to determine what trading action, if any, the writer clearly expresses or recommends.

## Data Source

The data came from the Reddit Finance Posts S&P 500 dataset created by Emil Partow and published on Hugging Face:

https://huggingface.co/datasets/emilpartow/reddit_finance_posts_sp500

The original dataset contains 431,923 Reddit posts collected from finance-related subreddits using the Reddit API and PRAW. Available fields include the post ID, title, body text, date, subreddit, and matched company keyword.

The source dataset was downloaded on October 5, 2026. Posts in our candidate pool were originally published between May 8, 2010 and July 2, 2025.

## What Each Instance Represents

Each row represents one finance-related Reddit post. The title and body were combined into one text field so annotators can read the available context in one place.

The annotation task is to determine whether the writer clearly expresses or recommends buying, selling, shorting, or holding an investment. Posts without one clear action receive the No Clear Trade Intent label.

## Candidate Pool

The initial candidate pool contains 800 posts from 15 finance-related subreddits. Each post has a unique item ID and unique text, and the pool contains no exact duplicate posts.

The posts contain between 3 and 100 words. The average length is approximately 39.4 words, and the median is 32 words.

### Candidate-Pool Columns

| Column | Description |
|---|---|
| `item_id` | Project-specific identifier, such as `RTI_0001` |
| `source_key` | Identifier from the original source dataset |
| `text` | Combined and cleaned Reddit title and body |
| `subreddit` | Subreddit where the post appeared |
| `company` | Company keyword matched by the original dataset |
| `created_datetime` | Date and time associated with the post |
| `word_count` | Number of words in the cleaned text |
| `label` | Human annotation; initially blank |

The `company` field is retained as source metadata but is not shown to annotators. During the pilot, we found that some company matches were inaccurate and could influence annotators unfairly.

## Annotation Dataset

After the internal pilot, 36 posts were automatically excluded because they had obvious quality problems. These included missing charts or images, automatic ticker tables, incomplete context, and extremely short or unclear text.

From the remaining candidates, 300 unique posts were selected for the planned annotation dataset:

- 50 shared agreement items
- 250 distributed coverage items

The 300 posts come from 15 subreddits. They contain between 5 and 100 words, with an average length of approximately 43.7 words and a median of 38.5 words. Their publication dates range from March 2, 2012 to July 2, 2025.

The five largest subreddit groups are:

| Subreddit | Posts |
|---|---:|
| `dividends` | 43 |
| `wallstreetbets` | 43 |
| `Superstonk` | 31 |
| `StockMarket` | 27 |
| `stocks` | 27 |

The remaining posts come from ETFs, RobinHood, investing, ValueInvesting, options, pennystocks, Forex, SecurityAnalysis, SPACs, and algotrading.

## Sampling Procedure

The first 800-post candidate pool was selected from the larger source dataset after combining titles and bodies, removing unusable records, cleaning the text, and removing duplicates. A fixed random seed was used so that the selection could be reproduced.

The internal pilot showed that simple random sampling produced many general discussion posts, no Hold labels, and relatively few clear Sell examples. It also revealed posts that depended on missing charts, images, or outside links.

For the final annotation setup, we retained general posts but also searched the candidate pool for possible Buy, Sell, Short, and Hold language. These keywords were used only to retrieve potentially useful candidates. They did not determine the labels. Human annotators will assign every final label using the written guidelines.

The shared agreement set was selected to contain clear actions, realistic No Clear Trade Intent cases, and the strongest available Hold examples. The distributed portion includes additional possible action candidates and randomly selected general posts. Unused candidate posts remain available as replacements.

Because this procedure intentionally increases the representation of possible trading intentions, the final label percentages should not be interpreted as the natural distribution of trading intentions across all Reddit finance posts.

## Cleaning and Privacy

The following processing was applied:

- Combined the Reddit title and body
- Removed web addresses and unnecessary Markdown formatting
- Replaced visible usernames and personal contact information
- Removed deleted, removed, empty, and duplicate records
- Limited text length
- Excluded obvious missing-context posts
- Excluded automatic ticker tables and similar generated reports
- Preserved financial terms, ticker symbols, slang, emojis, and original wording when possible

Annotators see only the project item ID and cleaned post text. They do not see usernames, links, company metadata, popularity scores, or preliminary sampling groups.

## Missing Data

The text, item ID, subreddit, creation date, and word-count fields are complete in both the candidate pool and annotation dataset. The label field is blank because the posts are initially unlabeled and will be labeled by human annotators.

Some posts may still contain unclear language or references that are difficult to understand. Annotators are instructed to report these cases using the item ID.

## Annotation Setup

Annotation is performed using Potato, a purpose-built annotation interface. Annotators see one post at a time and select exactly one of the four labels. The interface saves each annotator's selections in a structured output file.

The planned assignment design uses:

- 50 shared posts labeled by every external and internal annotator
- 50 additional non-overlapping posts per external annotator
- Approximately five external annotators and at least one internal annotator

With five external annotators, the shared posts may receive six labels each. These will support inter-annotator agreement and majority-vote or adjudicated ground truth. The distributed items increase overall coverage.

## Estimated Annotation Time

The internal pilot contained 50 posts. Potato recorded approximately 23.6 minutes of activity, or about 28 seconds per post. We therefore estimate that a typical post requires approximately 20–30 seconds to label.

An annotator should be able to label approximately 120–180 posts in one hour. The planned external assignment contains 100 posts, leaving time for difficult cases and reviewing the instructions.

## Reproduction Summary

To reproduce the dataset:

1. Download the source dataset from Hugging Face.
2. Combine the `title` and `text` fields.
3. Remove deleted, removed, empty, duplicate, and unusable records.
4. Remove URLs and unnecessary Markdown while preserving the original financial language.
5. Limit post length and remove obvious missing-context items.
6. Use a fixed random seed when sampling.
7. Retain general posts and retrieve additional candidate posts containing possible Buy, Sell, Short, or Hold language.
8. Leave all final labels blank until human annotation.

## License

The original Hugging Face dataset is distributed under the **Creative Commons Attribution 4.0 International license (CC BY 4.0)**. This derived dataset will use the same license and will provide attribution to the original dataset creator and source.

The license permits sharing and adaptation as long as appropriate attribution is provided:

https://creativecommons.org/licenses/by/4.0/

## Attribution

Original dataset: Emil Partow, *Reddit Finance Posts S&P 500*, Hugging Face.

https://huggingface.co/datasets/emilpartow/reddit_finance_posts_sp500
