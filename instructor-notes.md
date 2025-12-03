---
title: Instructor Notes
---

## Lesson motivation and learning objectives

Many researchers making the transition into genomics research (whether from another field or as their first research project) have
not had prior experience with command-line tools. They may quickly run into situations in which they need to use command-line tools
either because there is no good alternative for the type of analysis they want to do or because they have so many data files that doing
things manually on individual files is unfeasible.

This lesson will introduce learners to fundamental skills needed for working with their computers through a command-line interface (using
the bash shell). They will learn how to navigate their file system, computationally manipulate their files (e.g. copying, moving, renaming), search files, redirect output and write shell scripts. By the end of the lesson, learners will be prepared to move on to using more advanced bioinformatics command line tools (see the lesson on [Data Wrangling and Processing](https://www.datacarpentry.org/wrangling-genomics/)).

## Lesson design

This lesson is meant to be taught in its entirety. For novice learners, schedule around 4 hours for this lesson. If your learners are
already somewhat familiar with the bash shell, the earlier episodes can be condensed.

This lesson uses data hosted on an Amazon Machine Instance (AMI). Instructors will be sent information on how to log-in to the AMI by the workshop coordinator a few days before the workshop. If you are running a self-organized workshop, register the workshop with our [self-organized workshop form](https://amy.carpentries.org/forms/workshop/) and send us an email at [mailto:team@datacarpentry.org](mailto:team@datacarpentry.org) with information on how many people you expect to have at the workshop, and we'll start instances for you to use in the workshop. The day before the workshop, we'll send you the login information for your learners.

## Workshop Structure

### Timing per episode (draft 1)
- 01 Computing Concepts — 20 + 5
- 02 Introducing the Shell — 25 + 10
- 03 The Filesystem — 25 + 10
- 04 Working with Files — 25 + 15
- 05 Tidiness & Project Setup — 15 + 5
- 06 Project Planning — 15 + 5
- 07 Background: Sequencing & Genomics — 20 + 10
- 08 Quality Control — 25 + 15
- 09 Trimming — 20 + 10
- 10 Assembly with SPAdes — 30 + 25
- 11 Annotation with Prokka — 30 + 20
- 12 Review, Interpretation & Next Steps — 10 + 0 (optional capstone)

## Tips
- Keep shell lessons very tight.
- Allow time for in-person paper assembly activity before SPAdes.
- Expect delays during QC and trimming.


## Technical tips and tricks

### Etherpad template

There is a [template Etherpad](https://datacarpentry.org/shell-genomics/instructor/etherpad_template.html) to
paste into a collaborative document, such as the [Carpentries Etherpad](https://pad.carpentries.org/). Etherpad
supports synchronous document editing and is useful for collaborative work when teaching lessons.

#### Command Prompt Editing

Instructors might find it helpful to shorten their command prompt to allow better visibility of the commands they are typing, particularly if using the AMI.  This is because the prompt will contain additional information including the username and login for the instance, as well as filesystem location. This is especially useful when teaching the material online, as many learners may be splitting their screens and text wrapping may make the commands more difficult to identify if the prompt takes up a lot of space.

In order to edit your command prompt, type `PS1='$ '` into your shell and press enter. This will produce the simple "dollar space" prompt visible in the lesson content.

In order to reset the command prompt, type `source .bashrc` in order to source the bash profile, or type `PS1="\u@\h:\w $ "` in order to set the prompt to show username, "@", hostname, ":", and current working directory (ie. the user's current location within the filesystem).

NOTE: Editing the prompt is discussed in [1\. Introducing the Shell](https://datacarpentry.org/shell-genomics/01-introduction/index.html#navigating-your-file-system). This explains how to edit the prompt via `PS1='$ '` as here, so it would perhaps be best to *start* the lesson with the *default* prompt (as all the learners will and they can see that their screen will reassuringly match the instructor's screen at this point), and then instructors can choose to edit their prompt and talk through how they're doing that for learners' benefit at this section, or the instructor can just make the change early in the lesson for the visibility benefit, and explain to learners that they can find out how to do this in the lesson materials.

Resetting the command prompt is not currently included in the lesson materials, so it might be useful to be familiar with this beforehand in case of learners' questions.

## Common problems

This workshop introduces an analysis pipeline, where each step in that pipeline is dependent on the previous step.
If a learner gets behind, or one of the steps doesn't work for them, they may not be able to catch up with the rest of the class.
To help ensure that all learners are able to work through the whole process, we provide the solution files. This includes all
of the output files for each step in the data processing pipeline, as well as the scripts that the learners write collaboratively
with the Instructors throughout the workshop. These files are available on the AMI in `dcuser/.solutions`.

Similarly, if the learners aren't able to pull the data files that are pulled in the lesson directly from the SRA (e.g. due to
unstable internet), those files are available in the hidden backup directory (`dcuser/.backup`).

Make sure to tell your helpers about the `.solutions` and `.backup` directories so that they can use these resources to help
learners catch up during the workshop.


