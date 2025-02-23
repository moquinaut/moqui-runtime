# Components `runtime/component`

This directory contains three subfolders that designate components that are loaded when Moqui runs:

| Subfolder | Description                                                                                 |
|-----------|---------------------------------------------------------------------------------------------|
| addon     | Custom components that you create to address your business needs.                           |
| base      | Default components that come bundles with Moqui.                                            |
| external  | Components copied into a Docker container. This directory is mounted as a container volume. |
