# UnityNuGet Static

Place to hold several packages that are not provided with UnityNuGet registry (https://unitynuget-registry.openupm.com).

It's required to raise self-hosted UnityNuGet service for them now _(allowing to easily reference packages with up-to-date version)_.

Self-hosted registry with required packages was deployed on Google Cloud Run (https://unitynuget.tryapp.org/). But, unfortunately, the UnityNuGet startup process is too long _(even when packages was cached)_ and "Request-based" deploy doesn't fit _(Unity build fails to wait)_. So it's required to deploy the service as "Instance-based" that is much more expensive for really rare requests.

Solutions to solve the problem:
* Keep the packages in the project (horrible) or use another nuget delivery process _(i.e. NuGetForUnity)_
  * Not going to do as I think UPM-way is much better and easier to maintain
* Await packages are served on original UnityNuGet (https://github.com/bdovaz/UnityNuGet/pull/519)
  * But they don't satisfy current requirements and an issue was opened to solve this (https://github.com/bdovaz/UnityNuGet/issues/520)
* Optimize the UnityNuGet startup process allowing it to be used in Google Cloud Run "Request-based" deployments
  * Maybe I'll try in the future
* Replace a self-hosted UnityNuGet service hosting provider with another one _(possibly sharing instances with others required for development)_
  * Maybe as I'll discover and try different ones
* Quick workaround: reference packages in the unity-project explicitly as "git" packages
  * **This solution**
