---
title: Welcome to Quartz
draft: false
tags:
  - front-page
date: 2024-02-29
---

##  👋 Welcome

> [!Info]
> So, you've decided to level up your 🐍 game by installing a sense of formalism in your `dev` experience. Great! I'm excited for you. These docs will assist you in customizing [the repository factory](https://github.com/with-context-engine/repository-factory) to your specific needs and desired experience. 

## 🏛️ Repository *ethos*

We've all been there. Running `git init` and then 🤷🏽‍♂️ immediately thereafter. Questions like: 

1. Ok now how do I organize my python environment? 
2. Where do I place my files so that I can train, serve, deploy, or create something with python? 
3. Do I have the right dependencies? 
4. What about all the `bash` customizations I should use? 
5. Once I've got my ML code built, where do I go to train the model? 
6. How do I integrate these deployed tools (ML model, Streamlit app, FastAPI, etc., into my DevOps's environment?)
7. Whats a really clever way to involve CI/CD in this whole process so that I don't write brittle code? 

The list goes on and on. Finally, if you're interested in building actual machine learning *product prototypes*, you often wonder what's the best way to string together all these components? Well, that's the pain I've felt too. 

> Standing on the shoulders of [giants](https://github.com/radix-ai/poetry-cookiecutter/tree/main), [like](https://stefanbuck.com/blog/codeless-contributions-with-github-issue-forms), [these](https://stefanbuck.com/blog/repository-templates-meets-github-actions) guys, I've built this repository and documentation site to help you write the best code that DevOps and MLOps professionals will love. 

## Solution Architecture

This diagram documents how this repository behaves. It shows how all the components work together to form the basics of a modern ML application prototype. This repository can customize itself six different ways via `Cruft` and `Cookiecutter`. This means that this is a single repo that can create six different versions of itself to meet the needs of the developer.️ 

An example of how each customization might fit into a modern ML application like a chatbot deployed on Streamlit and backended by a trained chat model on Sagemaker is described below in the diagram. I will be referring to this diagram in each of the repository modes to denote how to customize it appropriately. 

![image](https://with-context-public.s3.us-east-1.amazonaws.com/repository-factory-docs/2024/19f85a0db6da482bf704b4a0a8460c4c.png)
### Pre-requisites

You will need an active working knowledge of and access to `git`, AWS, [DVC](http://dvc.org), and [Serverless](https://www.serverless.com/) in order to fully leverage this resource for your own benefit. At most you will need to create user accounts or assign IAM privileges to an account