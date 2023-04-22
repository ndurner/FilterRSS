# Filter RSS Feed with GPT-4

A Python script to filter an RSS feed by requesting relevance scores from GPT-4 and only including entries that meet a user-defined threshold.

## Usage

```
python filter_rss.py <rss_feed_path> <rss_dest_path> <system_prompt_path> [--threshold THRESHOLD]
```

- `rss_feed_path`: Path to the source RSS feed file.
- `rss_dest_path`: Path to the destination RSS feed file.
- `system_prompt_path`: Path to the text file containing the system prompt.
- `--threshold`: (Optional) Threshold for filtering entries based on GPT-4 score. Default is 0.5.

Before using this script, make sure you have set the `OPENAI_API_KEY` environment variable with your OpenAI API key.

## System Prompt
The text file referred to by system_prompt_path instructs GPT-4 to work as a content moderation system. This is a sample (also reproduced in sample-prompt.txt, ready to use):
```
You are a content moderation system. Rate the relevance of the input on a scale of 0 to 1. Only numbers are permitted replies. prioritize tweets that contain insightful, informative, or thought-provoking content. Avoid: overly promotional, political issues, platitudes, languages other than English or German.
```

To create a system prompt for GPT-4, you can use GPT-4 itself to learn from a few examples, like this:
```
You are given multiple user inputs which represent tweets to learn from. These are prefixed with either [WANTED] or [UNWANTED] for you, but these prefixes are not in the real data. From these inputs, create one System instruction for you, GPT-4, to use for future content ranking. This instruction only needs to be understandable by you. Tweets will be submitted individually to you, so while repetitive content is unwanted, you will not be able to infer it from the individual tweets.
```

Save the generated prompt in a text file and provide the path to the file when running the script.

## Dependencies

- [feedparser](https://pypi.org/project/feedparser/)
- [beautifulsoup4](https://pypi.org/project/beautifulsoup4/)
- [openai](https://pypi.org/project/openai/)

Install the dependencies using pip:

```
pip install feedparser beautifulsoup4 openai
```

## License

This project is licensed under the [GNU Affero General Public License v3.0](LICENSE) (AGPLv3). For more details, see the [LICENSE](LICENSE) file.