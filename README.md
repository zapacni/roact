<h1 align="center">Roact</h1>
<div align="center">
	<a href="https://travis-ci.org/Roblox/roact">
		<img src="https://api.travis-ci.org/Roblox/roact.svg?branch=master" alt="Travis-CI Build Status" />
	</a>
	<a href="https://coveralls.io/github/Roblox/roact?branch=master">
		<img src="https://coveralls.io/repos/github/Roblox/roact/badge.svg?branch=master" alt="Coveralls Coverage" />
	</a>
	<a href="https://roblox.github.io/roact">
		<img src="https://img.shields.io/badge/docs-website-green.svg" alt="Documentation" />
	</a>
</div>

<div align="center">
	A declarative view library for Roblox Lua inspired by <a href="https://reactjs.org">React</a>.
</div>

<div>&nbsp;</div>

## Installation

### Method 1: Model File (Roblox Studio)
* Download the `rbxmx` model file attached to the latest release from the [GitHub releases page](https://github.com/Roblox/Roact/releases).
* Insert the model into Studio into a place like `ReplicatedStorage`

### Method 2: Filesystem
* Copy the `lib` directory into your codebase
* Rename the folder to `Roact`
* Use a plugin like [Rojo](https://github.com/LPGhatguy/rojo) to sync the files into a place

## Usage
This sample creates a full-screen `TextLabel` with a greeting.

For more detailed examples, check out [the documentation](#).

```lua
local LocalPlayer = game:GetService("Players").LocalPlayer

local Roact = require(Roact)

-- Define a functional component
local function HelloComponent()
	-- createElement takes three arguments:
	-- * The type of element to make
	-- * Optionally, a list of properties to provide
	-- * Optionally, a dictionary of children. The key is that child's Name

	return Roact.createElement("ScreenGui", {
	}, {
		MainLabel = Roact.createElement("TextLabel", {
			Text = "Hello, world!",
			Size = UDim2.new(1, 0, 1, 0),
		}),
	})
end

-- Create our virtual tree
local root = Roact.createElement(HelloComponent)

-- Turn our virtual tree into real instances and put them in PlayerGui
Roact.reify(root, LocalPlayer.PlayerGui, "HelloWorld")
```

We can also write this example using a *stateful* component:

```lua
local LocalPlayer = game:GetService("Players").LocalPlayer

local Roact = require(Roact)

-- Create our component type
local HelloComponent = Roact.Component:extend("HelloComponent")

-- 'render' MUST be overridden.
function HelloComponent:render()
	-- createElement takes three arguments:
	-- * The type of element to make
	-- * Optionally, a list of properties to provide
	-- * Optionally, a dictionary of children. The key is that child's Name

	return Roact.createElement("ScreenGui", {
	}, {
		MainLabel = Roact.createElement("TextLabel", {
			Text = "Hello, world!",
			Size = UDim2.new(1, 0, 1, 0),
		}),
	})
end

-- Create our virtual tree
local root = Roact.createElement(HelloComponent)

-- Turn our virtual tree into real instances and put them in PlayerGui
Roact.reify(root, LocalPlayer.PlayerGui, "HelloWorld")
```

## License
Roact is available under the Apache 2.0 license. See [LICENSE](LICENSE) for details.