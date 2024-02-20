# gemini-testing
Jupyter notebook and associated chat history with Gemini Pro. Supporting Medium article https://medium.com/@its.jwho/errorhandling-vulnerability-tests-on-gemini-19601b246b52 published Feb 2024.

---

Error handling has long been one of the more tedious parts of any development endeavor. When teaching beginner Python courses, I feel time spent showing students when to create an exception for handling a specific error, and deciding what the program should return to the user for that error often falls short compared to its real-world importance. In part, this is due to over-used examples checking basics like division by 0 errors and validating string vs integer inputs from the command line. While error messages aim to provide developers with feedback to resolve issues and exception handling helps to ensure programs run smoothly - these very messages can often expose sensitive data.
This unintended information exposure compromises user privacy and security. When it comes to large language models applied across thousands of new applications and domains, this threat vector is more important than ever.

## Resources - Check my Work!
I've recorded all of my chat history and tuning settings for Gemini Pro on GitHub, which you can view in this repo. I wasn't interested in generating a viral, "gotcha" jailbreak-style attack, but rather examining how information contained in error messages from prompts sent to Gemini might leak information not otherwise intended to be disclosed in the LLM's response. In this regard, I do feel this exploration was successful.
- For ease of reading in this article, I've included screenshots of the actual Google Colab Enterprise notebook I used when working with the Gemini model for the first time. All of the screenshots at full resolution, a .py and .ipynb file of the notebook are also available in the GitHub repo.
- I've included footnotes to give additional background and resources that have proved helpful to me and my learning across this area.
- It's also important to note this work is a purely investigative and academic perspective, I did not receive and have not submitted anything contained within this article or the associated repo to a bug bounty program for AI vulnerabilities.
- I worked with Gemini exclusively through it's API via import vertexai and model = GenerativeModel("gemini-1.0-pro") as shown in the linked notebook.
Lastly, I didn't modify any of the standard response validation settings, which after doing a bit of reading, found that if you set response_validation=False when initiating a chat with Gemini, you may be able to allow "blocked or otherwise incomplete responses" into the chat history - which "might lead to future interactions being blocked by the service."

## TL;DR - Findings and Takeaway
Honestly, I didn't expect to find much while looking into adversarial attacks on a LLM as highly publicized, thoroughly researched, and expertly aligned model as Google's Gemini series. I was totally impressed by the speed, helpfulness, and overall safeguards of the model from a short time interacting with it. It's clear this LLM has been extensively aligned along Google's (AI Principles)[https://ai.google/responsibility/principles/] and (adversarial testing for generative AI safety)[https://blog.research.google/2023/11/responsible-ai-at-google-research_16.html] techniques.

> **That being said, I believe a opportunity for improvement, significant enough to merit additional review is needed when examining error messages returned by the model's infrastructure - specifically error messages returned in response to pushing the model to known adversarial or harmful boundaries.**
