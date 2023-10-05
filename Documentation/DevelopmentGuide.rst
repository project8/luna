Development Guide
=================

This guide is intended to help those keeping the Luna repository and the Luna containers up-to-date.

Implementing a luna_base Update
---------------------------------

We assume that luna_base has been updated, with a successful automated build of the luna_base container. 
And now you need to update everything else, update dependent dockerfiles, and get new images tagged and pushed.  
It's assumed that Katydid, Locust, and Mermithid all have automated builds when new versions are released.

1. Create a Release branch of Luna for the new Luna version.
2. Update the SoftwareVersions and ValidationLog documentation files with the new software versions.
3. Update the Luna version number in:
    * `Jupyter/Dockerfile` -- `ARG img_tag=`
4. Update the Katydid, Locust, and Mermithid Dockerfiles to use the new `luna_base` tag.
5. Release new (typically revision) versions of Katydid, Locust, and Mermithid.  Automated builds should start on GitHub Actions.
6. Update the luna_base version number in:
    * `Main/Dockerfile` -- `ARG img_tag=`
    * `.github/workflows/publish.yaml` -- `BASE_IMG_TAG:`
7.  Update the versions of Katydid, Locust, and Mermithid used in `Main/Dockerfile` (`ARG` lines)
8. Wait for and verify the Katydid, Locust, and Mermithid automated builds.
9. Make sure the Katydid, Locust, and Mermithid versions listed in SoftwareVersions and ValidationLog are correct since the new releases.
10. Create a pull request and check that the automated build works.
11. Merge the release branch and check that the automated build and push of containers works.
