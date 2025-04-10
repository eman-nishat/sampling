# ASSIGNMENT: Sampling and Reproducibility in Python

Read the blog post [Contact tracing can give a biased sample of COVID-19 cases](https://andrewwhitby.com/2020/11/24/contact-tracing-biased/) by Andrew Whitby to understand the context and motivation behind the simulation model we will be examining.

Examine the code in `whitby_covid_tracing.py`. Identify all stages at which sampling is occurring in the model. Describe in words the sampling procedure, referencing the functions used, sample size, sampling frame, any underlying distributions involved, and how these relate to the procedure outlined in the blog post.

Run the Python script file called whitby_covid_tracing.py as is and compare the results to the graphs in the original blog post. Does this code appear to reproduce the graphs from the original blog post?

Modify the number of repetitions in the simulation to 100 (from the original 1000). Run the script multiple times and observe the outputted graphs. Comment on the reproducibility of the results.

Alter the code so that it is reproducible. Describe the changes you made to the code and how they affected the reproducibility of the script file. The output does not need to match Whitby’s original blogpost/graphs, it just needs to produce the same output when run multiple times

# Author: Eman Nishat

```
Sampling first occurs when a random subset of people are infected using np.random.choice(). Since replace=FALSE, this function is using simple random sampling without replacement. The sample size of this random subset is 100, and the sampling frame is all attendees for both weddings and brunches. The distribution involved here is uniform random selection since each person has an equal chance of being infected. Then, sampling is done to decide which infected people get traced using the function np.random.rand(). The sample size is approximately 20 and the sampling frame is only the people that were infected. The distribution involved here is Bernoulli distribution. Next, sampling is done to determine which events undergo secondary contact tracing. This is done with the function value_counts(). Here, if an event has at least two infected people that have been traced, then all infected attendees are marked as traced. This creates a selection bias since attendees for smaller events are more likely to pass the threshold due to the smaller group size. The sample size can vary and sample frame is all infected attendees at events where at least two people were traced. The distribution is threshold-based selection.

When running the Python script, the resulting graph does not exactly reproduce the graphs from the original blog post. This is due to the random sampling of people that are infected. Since there was no random seed set, the people infected can change. The subsequent portions of the code which decides which people get traced and secondary traced then depends on the initial infected sample.

After modifying the number of repetitions in the simulation to 100 and running the script multiple times, it is evident that the results are not reproducible since the histograms are different each time both for the infections from weddings and traced to weddings. This further demonstrates how a small sample size can introduce more variability.

To make the code reproducible, I added a random seed at the top of the script: np.random.seed(123). This ensures that the output is the same every time the script is run. If someone else wanted to reproduce the same results, they would have to use the same seed.

```


## Criteria

|Criteria|Complete|Incomplete|
|--------|----|----|
|Altercation of the code|The code changes made, made it reproducible.|The code is still not reproducible.|
|Description of changes|The author explained the reasonings for the changes made well.|The author did not explain the reasonings for the changes made well.|

## Submission Information

🚨 **Please review our [Assignment Submission Guide](https://github.com/UofT-DSI/onboarding/blob/main/onboarding_documents/submissions.md)** 🚨 for detailed instructions on how to format, branch, and submit your work. Following these guidelines is crucial for your submissions to be evaluated correctly.

### Submission Parameters:
* Submission Due Date: `23:59 - 09/04/2025`
* The branch name for your repo should be: `assignment-1`
* What to submit for this assignment:
    * This markdown file (a1_sampling_and_reproducibility.md) should be populated.
    * The `whitby_covid_tracing.py` should be changed.
* What the pull request link should look like for this assignment: `https://github.com/<your_github_username>/sampling/pull/<pr_id>`
    * Open a private window in your browser. Copy and paste the link to your pull request into the address bar. Make sure you can see your pull request properly. This helps the technical facilitator and learning support staff review your submission easily.

Checklist:
- [ ] Create a branch called `assignment-1`.
- [ ] Ensure that the repository is public.
- [ ] Review [the PR description guidelines](https://github.com/UofT-DSI/onboarding/blob/main/onboarding_documents/submissions.md#guidelines-for-pull-request-descriptions) and adhere to them.
- [ ] Verify that the link is accessible in a private browser window.

If you encounter any difficulties or have questions, please don't hesitate to reach out to our team via the help channel in Slack. Our Technical Facilitators and Learning Support staff are here to help you navigate any challenges.
