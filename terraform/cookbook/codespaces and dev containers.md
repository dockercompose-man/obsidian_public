# 3.1 Codespaces and Dev Containers

You need to be able to code while mobile and away from your standard office setting.

Working on problems in the comfortable space of your office can make your infrastructure as code sessions quite lovely. Maybe you have a favorite artist you listen to while you work or a chillwave playlist from Spotify. When you need to leave the comfort of your office, you can be left in the lurch with your coding environment when you’re moving or traveling. Not everyone can bring their desktop machine or coding workstation with them, and this recipe is for anyone on the go or who favors moving their workspace entirely into the cloud.

## Solution

Getting this recipe working contains quite a few steps, so buckle up and prepare for all these moving parts. Wel’ll be using [GitHub](https://github.com/), [Visual Studio Code](https://code.visualstudio.com/) (VSC), and a browser to complete these steps, so be sure to sign up and download those as you need.

To begin, create a .devcontainer folder at the root of your directory, then an empty Dockerfile and devcontainer.json file (Figure 3-1).

.devcontainer
	devcontainer.json
	Dockerfile

# See https://hub.docker.com/r/hashicorp/terraform for more information
FROM hashicorp/terraform:1.2.6

Next, we specify the JSON configuration for how our codespace container will work in the devcontainer.json file, with the following lines.

// For format details, see https://aka.ms/devcontainer.json. For config options, see the README at:
// https://github.com/microsoft/vscode-dev-containers/tree/v0.238.1/containers/codespaces-linux

```ruby
{
	"name": "GitHub Codespaces (Default)",
	"build": {
		"dockerfile": "Dockerfile"
	},
	// Configure tool-specific properties.
	"customizations": {
		// Configure properties specific to VS Code.
		"vscode": {
			// Add the IDs of extensions you want installed when the container is created.
			"extensions": [
				"GitHub.vscode-pull-request-github",
        "GitHub.copilot",
        "HashiCorp.terraform"
			]
		}
	}
}
```

Now, commit and push your changes to the repository you’re working with on GitHub.

###### NOTE

Ensure that your changes are pushed to GitHub or these next steps will not work.

Once your code is on GitHub, you will notice that you have unlocked a new capability, CodeSpaces.

To create your codespace, you can use the button within the GitHub UI (Figure 3-2), or you can try some of the other [creation options](https://github.com/features/codespaces).