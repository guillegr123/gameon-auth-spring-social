# Spring Social GameOn Auth.

Implementation of GameOn Auth project, using Spring Social. 

*INCOMPLETE::* Work in progress, but basic concepts proven. =)

## Overview

Initial Urls:
- `/auth/facebook`
- `/auth/twitter`
- `/auth/github?scope=user:email`
- `/auth/google?scope=profile%20email`

Redirect Urls: (for configuring within social apps, prefix the host/port of this app)
- `/auth/facebook`
- `/auth/twitter`
- `/auth/github`
- `/auth/google`

## Flow:

Browser goes to appropriate initial url, gets bounced to remote service to sign in, then back to redirect url, which reads tokens etc, and forwards browser to `/token` endpoint. 

`/token` endpoint is a RestController, that uses spring social to obtain the connection and then uses that to pull unique Id, name, and email.

Where possible this uses standard spring social stuff to do its job. This works as expected for Facebook, and Google, and is pretty straight forward.

GitHub and Twitter were oddly annoying re email, and needed invocation of new endpoints, so the 
appropriate Template has to be instantiated, and used to get the reply. Corresponding Java bindings
for the reply JSON are in the model package. 

*TODO*

- Update yaml's to pull the social creds from env vars.
- Have `/token` endpoint controller create and sign a jwt as the old GameOn Auth used to. 
- Have `/token` endpoint foward to the auth success url appending the token
- Add gameon auth service compatible initial url rest handler that replies with redirects to the new initial urls?
- Dockerise the whole thing using Game On Auth as a template.
- Tests? Maybe?
- Trvais build etc.



