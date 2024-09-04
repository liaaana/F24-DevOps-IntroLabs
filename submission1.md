# Benefits of signing commits

Signing commits improves the **code's security** and has **several benefits**:

1) **Trust and reputation**: Signing commits gives others confidence that the modifications were indeed made by the author of the commit. This verification is essential to preserving trust and reputation, particularly in case someone tries to exploit the author's identity fraudulently to insert dangerous code.
2) **Local storage of key**: GitHub is unable to sign commits on behalf of users because it lacks access to the committer's private signing keys. The security of commits is enhanced since only the author has access to the signing key by keeping it locally.


# Merge Strategies

**Merging** is the process of combining branches in Git. Git offers several merge strategies for handling branch merging.
## Standard Merge
Creates a new commit, known as a "merge commit," which represents the combination of two branches. This process merges a feature branch into the main branch by incorporating all changes from the feature branch into a new commit on the base branch.

| **Advantages**                                                                                                                                             | **Disadvantages**                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------- |
| Provides a clearer development history with a detailed graph showing where branches were merged, preserving the history of changes in the merged branches. | Commit history can become noisy due to numerous merge commits from small branches. |
| Useful for team collaboration by maintaining a structured record of changes.                                                                               | A complex commit graph may make it harder to understand the project context.       |
**Standard merging** technique is **usually chosen for collaboration**. It's main advantage is that It keeps a thorough history of all modifications, which is helpful to understand how a project has changed over time. Such history provides a simpler conditions to resolve conflicts and guarantees that everyone who works on project understands how project changed over the time.

## Squash and Merge
Before merging a feature branch's changes into the main branch, they are combined into a single commit. The base branch then has this unified commit added to it. In a such way commit history become simpler.

| **Advantages**                                                                                                                 | **Disadvantages**                                      |
| ------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------ |
| Cleaner and linear commit history that makes navigation easier and reduce the noise compared to standard merge strategy.       | Loss of detailed commit history of the feature branch. |
| Works very good when feature branches with lots of small contributions are merged together, main branch become more organised. | Tracking of specific changes become harder.            |

## Rebase and Merge
Feature branch's commits are reapplied on top of the base branch prior to merging it into the base branch. Commit history is rewritten to make it look as though the feature branch changes were applied over the base branch.

| **Advantages**                                                                         | **Disadvantages**                                               |
| -------------------------------------------------------------------------------------- | --------------------------------------------------------------- |
| Removing merge commits helps to make history cleaner with no noise from merge commits. | Navigation problems due to the absence of merging commits.      |
| Understanding the development process is easier because of linear history.             | Harder to roll back changes if the feature is no longer needed. |
