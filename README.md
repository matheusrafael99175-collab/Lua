<!DOCTYPE html>
<html lang="en">

<head>
 <meta charset="UTF-8">
 <title>Script Bot F3X</title>
 <style>
  body { background:#111; color:#0f0; font-family:monospace; text-align:center; padding:30px; }
  input, button { padding:10px; font-size:16px; margin:5px; }
  textarea { width:90%; height:300px; background:#000; color:#0f0; border:1px solid #0f0; margin-top:10px; white-space: pre; overflow-x: auto; }
  #command-list { max-height:200px; overflow-y:auto; text-align:left; width:90%; margin:10px auto; border:1px solid #0f0; padding:5px; }
  #footer { margin-top:20px; font-size:14px; color:#0f0; }
 </style>
</head>

<body>

 <h2>Script Bot F3X </h2>

 <input id="search" placeholder="Search commands..." oninput="filterCommands()">
 <br>
 <input id="cmd" placeholder="Type a command like /sky or /decal">
 <button onclick="run()">Show Script</button>
 <button onclick="copyScript()">Copy</button>
 <button onclick="downloadScript()">Download TXT</button>

 <textarea id="out" readonly></textarea>

 <div id="command-list">
  <p>/sky - Skybox f3x</p>
  <p>/decal - Decal spam f3x</p>
  <p>/btools - get btools</p>
  <p>/disco</p>
  <p>/fire-all - 666</p>
  <p>/realm - You can edit this realm script.</p>
  <p>/spin-all</p>
  <p>/fire-parts</p>
  <p>/mario.exe</p>
  <p>/baseplate</p>
  <p>/unanchor</p>
  <p>/skys - sky spin</p>
  <p>/skyw - It's a Sky TV that keeps flashing with HD Admin</p>
  <p>/particles</p>
 </div>

 <script>
  // Aqui vocÃª coloca os scripts longos
  const commands = {
    "sky": `
  local player = game.Players.LocalPlayer
  		local char = player.Character
  		local backpack = player.Backpack
  	
  		local function getf3x()
  			for _, v in ipairs(backpack:GetChildren()) do
  				if v:FindFirstChild("SyncAPI") then
  					return v
  				end
  			end
  			for _, v in ipairs(char:GetChildren()) do
  				if v:FindFirstChild("SyncAPI") then
  					return v
  				end
  			end
  	
  			return nil
  		end
  	
  		-- get all info
  	
  		local f3x = getf3x()
  		if not f3x then
  			warn("you dont have f3x skid")
  		end
  		local syncapi = f3x.SyncAPI
  		local serverendpoint = syncapi.ServerEndpoint
  	
  		-- name func
  	
  		local function name(part, stringa)
  			local args = {
  				[1] = "SetName",
  				[2] = {
  					[1] = part
  				},
  				[3] = stringa
  			}
  			serverendpoint:InvokeServer(unpack(args))
  		end
  		
  		local function setcollision(part, booleana)
  			local args = {
  				[1] = "SyncCollision",
  				[2] = {
  					[1] = {
  						["Part"] = part,
  						["CanCollide"] = booleana
  					}
  				}
  			}
  			serverendpoint:InvokeServer(unpack(args))
  		end
  	
  		local function lock(part, boolean)
  			local args = {
  				[1] = "SetLocked",
  				[2] = {
  					[1] = part
  				},
  				[3] = boolean
  			}
  			serverendpoint:InvokeServer(unpack(args))
  		end
  	
  		-- sky func
  	
  		local function sky()
  			spawn(function()
  				local position = char.Head.Position
  				local part = serverendpoint:InvokeServer("CreatePart", "Normal", CFrame.new(position + Vector3.new(0, 2, 0)), workspace)
  				local args = {
  					[1] = "CreateMeshes",
  					[2] = {
  						[1] = {
  							["Part"] = part
  						}
  					}
  				}
  				serverendpoint:InvokeServer(unpack(args))
  				local args = {
  					[1] = "SyncMesh",
  					[2] = {
  						[1] = {
  							["Part"] = part,
  							["MeshId"] = "rbxassetid://8006679977"
  						}
  					}
  				}
  				serverendpoint:InvokeServer(unpack(args))
  				local args = {
  					[1] = "SyncMesh",
  					[2] = {
  						[1] = {
  							["Part"] = part,
  							["Scale"] = Vector3.new(90, 90, 90)
  						}
  					}
  				}
  				serverendpoint:InvokeServer(unpack(args))
  				local args = {
  					[1] = "SyncMesh",
  					[2] = {
  						[1] = {
  							["Part"] = part,
  							["TextureId"] =	"rbxassetid://ID"
  						}
  					}
  				}
  				serverendpoint:InvokeServer(unpack(args))
  	
  				name(part, "Sky")
  				lock(part, true)
  				setcollision(part, false)
  			end)
  		end
  	
  		sky()
  `,
    "decal": `
  local player = game.Players.LocalPlayer
  		local char = player.Character
  		local backpack = player.Backpack
  	
  		local function getf3x()
  			for _, v in ipairs(backpack:GetChildren()) do
  				if v:FindFirstChild("SyncAPI") then
  					return v
  				end
  			end
  			for _, v in ipairs(char:GetChildren()) do
  				if v:FindFirstChild("SyncAPI") then
  					return v
  				end
  			end
  	
  			return nil
  		end
  	
  		-- get all info
  	
  		local f3x = getf3x()
  		if not f3x then
  			warn("you dont have f3x skid")
  		end
  		local syncapi = f3x.SyncAPI
  		local serverendpoint = syncapi.ServerEndpoint
  	
  		local function createdecal(part, side)
  			local args = {
  				[1] = "CreateTextures",
  				[2] = {
  					[1] = {
  						["Part"] = part,
  						["Face"] = side,
  						["TextureType"] = "Decal"
  					}
  				}
  			}
  			serverendpoint:InvokeServer(unpack(args))
  		end
  		local function setdecal(part, asset, side)
  			local args = {
  				[1] = "SyncTexture",
  				[2] = {
  					[1] = {
  						["Part"] = part,
  						["Face"] = side,
  						["TextureType"] = "Decal",
  						["Texture"] = "rbxassetid://".. asset
  					}
  				}
  			}
  			serverendpoint:InvokeServer(unpack(args))
  		end
  	
  		local function decalspam()
  			local decalid = ID
  			for _, v in ipairs(workspace:GetDescendants()) do
  				if v:IsA("BasePart") or v:IsA("UnionOperation") then
  					spawn(function()
  						createdecal(v, Enum.NormalId.Front)
  						createdecal(v, Enum.NormalId.Back)
  						createdecal(v, Enum.NormalId.Left)
  						createdecal(v, Enum.NormalId.Right)
  						createdecal(v, Enum.NormalId.Bottom)
  						createdecal(v, Enum.NormalId.Top)
  	
  						setdecal(v, decalid, Enum.NormalId.Front)
  						setdecal(v, decalid, Enum.NormalId.Back)
  						setdecal(v, decalid, Enum.NormalId.Left)
  						setdecal(v, decalid, Enum.NormalId.Right)
  						setdecal(v, decalid, Enum.NormalId.Bottom)
  						setdecal(v, decalid, Enum.NormalId.Top)
  					end)
  				end
  			end
  		end
  	
  		decalspam()
  `,
    "btools": `
  local ReplicatedStorage = game:GetService("ReplicatedStorage")
  	local RequestCommand = ReplicatedStorage:WaitForChild("HDAdminHDClient").Signals.RequestCommandSilent
  
  	RequestCommand:InvokeServer(";btools")
  `,
    "disco": `
  local ReplicatedStorage = game:GetService("ReplicatedStorage")
  	local RequestCommand = ReplicatedStorage:WaitForChild("HDAdminHDClient").Signals.RequestCommandSilent
  
  	RequestCommand:InvokeServer(";disco")
  `,
    "fire-all": `
  local player = game.Players.LocalPlayer
  	local char = player.Character
  	local tool
  	for i,v in player:GetDescendants() do
  		if v.Name == "SyncAPI" then
  			tool = v.Parent
  		end
  	end
  	for i,v in game.ReplicatedStorage:GetDescendants() do
  		if v.Name == "SyncAPI" then
  			tool = v.Parent
  		end
  	end
  	--craaa
  	remote = tool.SyncAPI.ServerEndpoint
  	function _(args)
  		remote:InvokeServer(unpack(args))
  	end
  	function SetCollision(part,boolean)
  		local args = {
  			[1] = "SyncCollision",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["CanCollide"] = boolean
  				}
  			}
  		}
  		_(args)
  	end
  	function SetAnchor(boolean,part)
  		local args = {
  			[1] = "SyncAnchor",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["Anchored"] = boolean
  				}
  			}
  		}
  		_(args)
  	end
  	function CreatePart(cf,parent)
  		local args = {
  			[1] = "CreatePart",
  			[2] = "Normal",
  			[3] = cf,
  			[4] = parent
  		}
  		_(args)
  	end
  	function DestroyPart(part)
  		local args = {
  			[1] = "Remove",
  			[2] = {
  				[1] = part
  			}
  		}
  		_(args)
  	end
  	function MovePart(part,cf)
  		local args = {
  			[1] = "SyncMove",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["CFrame"] = cf
  				}
  			}
  		}
  		_(args)
  	end
  	function Resize(part,size,cf)
  		local args = {
  			[1] = "SyncResize",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["CFrame"] = cf,
  					["Size"] = size
  				}
  			}
  		}
  		_(args)
  	end
  	function AddMesh(part)
  		local args = {
  			[1] = "CreateMeshes",
  			[2] = {
  				[1] = {
  					["Part"] = part
  				}
  			}
  		}
  		_(args)
  	end
  
  	function SetMesh(part,meshid)
  		local args = {
  			[1] = "SyncMesh",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["MeshId"] = "rbxassetid://"..meshid
  				}
  			}
  		}
  		_(args)
  	end
  	function SetTexture(part, texid)
  		local args = {
  			[1] = "SyncMesh",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["TextureId"] = "rbxassetid://"..texid
  				}
  			}
  		}
  		_(args)
  	end
  	function SetName(part, stringg)
  		local args = {
  			[1] = "SetName",
  			[2] = {
  				[1] = part
  			},
  			[3] = stringg
  		}
  
  		_(args)
  	end
  	function MeshResize(part,size)
  		local args = {
  			[1] = "SyncMesh",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["Scale"] = size
  				}
  			}
  		}
  		_(args)
  	end
  	function Weld(part1, part2,lead)
  		local args = {
  			[1] = "CreateWelds",
  			[2] = {
  				[1] = part1,
  				[2] = part2
  			},
  			[3] = lead
  		}
  		_(args)
  
  	end
  	function SetLocked(part,boolean)
  		local args = {
  			[1] = "SetLocked",
  			[2] = {
  				[1] = part
  			},
  			[3] = boolean
  		}
  		_(args)
  	end
  	function SetTrans(part,int)
  		local args = {
  			[1] = "SyncMaterial",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["Transparency"] = int
  				}
  			}
  		}
  		_(args)
  	end
  	function CreateSpotlight(part)
  		local args = {
  			[1] = "CreateLights",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["LightType"] = "SpotLight"
  				}
  			}
  		}
  		_(args)
  	end
  	function SyncLighting(part,brightness)
  		local args = {
  			[1] = "SyncLighting",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["LightType"] = "SpotLight",
  					["Brightness"] = brightness
  				}
  			}
  		}
  		_(args)
  	end
  	function Color(part,color)
  		local args = {
  			[1] = "SyncColor",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["Color"] = color --[[Color3]],
  					["UnionColoring"] = false
  				}
  			}
  		}
  		_(args)
  	end
  	function SpawnDecal(part,side)
  		local args = {
  			[1] = "CreateTextures",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["Face"] = side,
  					["TextureType"] = "Decal"
  				}
  			}
  		}
  
  		_(args)
  	end
  	function AddDecal(part,asset,side)
  		local args = {
  			[1] = "SyncTexture",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["Face"] = side,
  					["TextureType"] = "Decal",
  					["Texture"] = "rbxassetid://".. asset
  				}
  			}
  		}
  		_(args)
  	end
  
  	function Sky(id)
  		e = char.HumanoidRootPart.CFrame.x
  		f = char.HumanoidRootPart.CFrame.y
  		g = char.HumanoidRootPart.CFrame.z
  		CreatePart(CFrame.new(math.floor(e),math.floor(f),math.floor(g)) + Vector3.new(0,6,0),workspace)
  		for i,v in game.Workspace:GetDescendants() do
  			if v:IsA("BasePart") and v.CFrame.x == math.floor(e) and v.CFrame.z == math.floor(g) then
  				--spawn(function()
  				SetName(v,"Sky")
  				AddMesh(v)
  				--end)
  				--spawn(function()
  				SetMesh(v,"8006679977")
  				SetTexture(v,id)
  				--end)
  				MeshResize(v,Vector3.new(50,50,50))
  				SetLocked(v,true)
  			end
  		end
  	end
  	Sky("16028663795")
  
  	-----------------------------------
  
  	local player = game.Players.LocalPlayer
  	local char = player.Character
  	local tool
  	for i,v in player:GetDescendants() do
  		if v.Name == "SyncAPI" then
  			tool = v.Parent
  		end
  	end
  	for i,v in game.ReplicatedStorage:GetDescendants() do
  		if v.Name == "SyncAPI" then
  			tool = v.Parent
  		end
  	end
  	--craaa
  	remote = tool.SyncAPI.ServerEndpoint
  	function _(args)
  		remote:InvokeServer(unpack(args))
  	end
  	function SetCollision(part,boolean)
  		local args = {
  			[1] = "SyncCollision",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["CanCollide"] = boolean
  				}
  			}
  		}
  		_(args)
  	end
  	function SetAnchor(boolean,part)
  		local args = {
  			[1] = "SyncAnchor",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["Anchored"] = boolean
  				}
  			}
  		}
  		_(args)
  	end
  	function CreatePart(cf,parent)
  		local args = {
  			[1] = "CreatePart",
  			[2] = "Normal",
  			[3] = cf,
  			[4] = parent
  		}
  		_(args)
  	end
  	function DestroyPart(part)
  		local args = {
  			[1] = "Remove",
  			[2] = {
  				[1] = part
  			}
  		}
  		_(args)
  	end
  	function MovePart(part,cf)
  		local args = {
  			[1] = "SyncMove",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["CFrame"] = cf
  				}
  			}
  		}
  		_(args)
  	end
  	function Resize(part,size,cf)
  		local args = {
  			[1] = "SyncResize",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["CFrame"] = cf,
  					["Size"] = size
  				}
  			}
  		}
  		_(args)
  	end
  	function AddMesh(part)
  		local args = {
  			[1] = "CreateMeshes",
  			[2] = {
  				[1] = {
  					["Part"] = part
  				}
  			}
  		}
  		_(args)
  	end
  
  	function SetMesh(part,meshid)
  		local args = {
  			[1] = "SyncMesh",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["MeshId"] = "rbxassetid://"..meshid
  				}
  			}
  		}
  		_(args)
  	end
  	function SetTexture(part, texid)
  		local args = {
  			[1] = "SyncMesh",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["TextureId"] = "rbxassetid://"..texid
  				}
  			}
  		}
  		_(args)
  	end
  	function SetName(part, stringg)
  		local args = {
  			[1] = "SetName",
  			[2] = {
  				[1] = part
  			},
  			[3] = stringg
  		}
  
  		_(args)
  	end
  	function MeshResize(part,size)
  		local args = {
  			[1] = "SyncMesh",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["Scale"] = size
  				}
  			}
  		}
  		_(args)
  	end
  	function Weld(part1, part2,lead)
  		local args = {
  			[1] = "CreateWelds",
  			[2] = {
  				[1] = part1,
  				[2] = part2
  			},
  			[3] = lead
  		}
  		_(args)
  
  	end
  	function SetLocked(part,boolean)
  		local args = {
  			[1] = "SetLocked",
  			[2] = {
  				[1] = part
  			},
  			[3] = boolean
  		}
  		_(args)
  	end
  	function SetTrans(part,int)
  		local args = {
  			[1] = "SyncMaterial",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["Transparency"] = int
  				}
  			}
  		}
  		_(args)
  	end
  	function CreateSpotlight(part)
  		local args = {
  			[1] = "CreateLights",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["LightType"] = "SpotLight"
  				}
  			}
  		}
  		_(args)
  	end
  	function SyncLighting(part,brightness)
  		local args = {
  			[1] = "SyncLighting",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["LightType"] = "SpotLight",
  					["Brightness"] = brightness
  				}
  			}
  		}
  		_(args)
  	end
  	function Color(part,color)
  		local args = {
  			[1] = "SyncColor",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["Color"] = color --[[Color3]],
  					["UnionColoring"] = false
  				}
  			}
  		}
  		_(args)
  	end
  	function SpawnDecal(part,side)
  		local args = {
  			[1] = "CreateTextures",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["Face"] = side,
  					["TextureType"] = "Decal"
  				}
  			}
  		}
  
  		_(args)
  	end
  	function AddDecal(part,asset,side)
  		local args = {
  			[1] = "SyncTexture",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["Face"] = side,
  					["TextureType"] = "Decal",
  					["Texture"] = "rbxassetid://".. asset
  				}
  			}
  		}
  		_(args)
  	end
  
  	function spam(id)
  		for i,v in game.workspace:GetDescendants() do
  			if v:IsA("BasePart") then
  				spawn(function()
  					SetLocked(v,false)
  					SpawnDecal(v,Enum.NormalId.Front)
  					AddDecal(v,id,Enum.NormalId.Front)
  
  					SpawnDecal(v,Enum.NormalId.Back)
  					AddDecal(v,id,Enum.NormalId.Back)
  
  					SpawnDecal(v,Enum.NormalId.Right)
  					AddDecal(v,id,Enum.NormalId.Right)
  
  					SpawnDecal(v,Enum.NormalId.Left)
  					AddDecal(v,id,Enum.NormalId.Left)
  
  					SpawnDecal(v,Enum.NormalId.Bottom)
  					AddDecal(v,id,Enum.NormalId.Bottom)
  
  					SpawnDecal(v,Enum.NormalId.Top)
  					AddDecal(v,id,Enum.NormalId.Top)
  				end)
  			end
  		end 
  	end
  	spam("16028663795")
  
  	-----------
  
  	local player = game.Players.LocalPlayer
  	local char = player.Character
  	local tool
  	for i,v in player:GetDescendants() do
  		if v.Name == "SyncAPI" then
  			tool = v.Parent
  		end
  	end
  	for i,v in game.ReplicatedStorage:GetDescendants() do
  		if v.Name == "SyncAPI" then
  			tool = v.Parent
  		end
  	end
  	--craaa
  	remote = tool.SyncAPI.ServerEndpoint
  	function _(args)
  		remote:InvokeServer(unpack(args))
  	end
  	function SetCollision(part,boolean)
  		local args = {
  			[1] = "SyncCollision",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["CanCollide"] = boolean
  				}
  			}
  		}
  		_(args)
  	end
  	function SetAnchor(boolean,part)
  		local args = {
  			[1] = "SyncAnchor",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["Anchored"] = boolean
  				}
  			}
  		}
  		_(args)
  	end
  	function CreatePart(cf,parent)
  		local args = {
  			[1] = "CreatePart",
  			[2] = "Normal",
  			[3] = cf,
  			[4] = parent
  		}
  		_(args)
  	end
  	function DestroyPart(part)
  		local args = {
  			[1] = "Remove",
  			[2] = {
  				[1] = part
  			}
  		}
  		_(args)
  	end
  	function MovePart(part,cf)
  		local args = {
  			[1] = "SyncMove",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["CFrame"] = cf
  				}
  			}
  		}
  		_(args)
  	end
  	function Resize(part,size,cf)
  		local args = {
  			[1] = "SyncResize",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["CFrame"] = cf,
  					["Size"] = size
  				}
  			}
  		}
  		_(args)
  	end
  	function AddMesh(part)
  		local args = {
  			[1] = "CreateMeshes",
  			[2] = {
  				[1] = {
  					["Part"] = part
  				}
  			}
  		}
  		_(args)
  	end
  
  	function SetMesh(part,meshid)
  		local args = {
  			[1] = "SyncMesh",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["MeshId"] = "rbxassetid://"..meshid
  				}
  			}
  		}
  		_(args)
  	end
  	function SetTexture(part, texid)
  		local args = {
  			[1] = "SyncMesh",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["TextureId"] = "rbxassetid://"..texid
  				}
  			}
  		}
  		_(args)
  	end
  	function SetName(part, stringg)
  		local args = {
  			[1] = "SetName",
  			[2] = {
  				[1] = workspace.Part
  			},
  			[3] = stringg
  		}
  
  		_(args)
  	end
  	function MeshResize(part,size)
  		local args = {
  			[1] = "SyncMesh",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["Scale"] = size
  				}
  			}
  		}
  		_(args)
  	end
  	function Weld(part1, part2,lead)
  		local args = {
  			[1] = "CreateWelds",
  			[2] = {
  				[1] = part1,
  				[2] = part2
  			},
  			[3] = lead
  		}
  		_(args)
  
  	end
  	function SetLocked(part,boolean)
  		local args = {
  			[1] = "SetLocked",
  			[2] = {
  				[1] = part
  			},
  			[3] = boolean
  		}
  		_(args)
  	end
  	function SetTrans(part,int)
  		local args = {
  			[1] = "SyncMaterial",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["Transparency"] = int
  				}
  			}
  		}
  		_(args)
  	end
  	function CreateSpotlight(part)
  		local args = {
  			[1] = "CreateLights",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["LightType"] = "SpotLight"
  				}
  			}
  		}
  		_(args)
  	end
  	function SyncLighting(part,brightness)
  		local args = {
  			[1] = "SyncLighting",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["LightType"] = "SpotLight",
  					["Brightness"] = brightness
  				}
  			}
  		}
  		_(args)
  	end
  	function AddFire(part)
  		local args = {
  			[1] = "CreateDecorations",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["DecorationType"] = "Fire"
  				}
  			}
  		}
  		_(args)
  	end
  	function sixsixsix()
  		for i,v in game.Workspace:GetDescendants() do
  			spawn(function()
  				SetLocked(v,false)
  				AddFire(v)
  			end)
  		end
  	end
  	sixsixsix()
  `,
    "realm": `
  local ReplicatedStorage = game:GetService("ReplicatedStorage")
  	local RequestCommand = ReplicatedStorage:WaitForChild("HDAdminHDClient").Signals.RequestCommandSilent
  	RequestCommand:InvokeServer(";btools me")
      RequestCommand:InvokeServer(";fogcolor black")
  	wait(0.4)
  	RequestCommand:InvokeServer(";punish all")
  	wait(0.1)
  	local player = game.Players.LocalPlayer
  	local char = player.Character
  	local backpack = player.Backpack
  
  	local function getf3x()
  		for _, v in ipairs(backpack:GetChildren()) do
  			if v:FindFirstChild("SyncAPI") then
  				return v
  			end
  		end
  		for _, v in ipairs(char:GetChildren()) do
  			if v:FindFirstChild("SyncAPI") then
  				return v
  			end
  		end
  
  		return nil
  	end
  	local f3x = getf3x()
  	if not f3x then
  		warn("you dont have f3x skid")
  	end
  	local syncapi = f3x.SyncAPI
  	local serverendpoint = syncapi.ServerEndpoint
  
  	local function delete(part)
  		local args = {
  			[1] = "Remove",
  			[2] = {
  				[1] = part
  			}
  		}
  		serverendpoint:InvokeServer(unpack(args))
  	end
  
  	local function deleteall()
  		for _, v in ipairs(workspace:GetDescendants()) do
  			if v:IsA("BasePart") or v:IsA("UnionOperation") then
  				spawn(function()
  					delete(v)
  				end)
  			end
  		end
  	end
  
  	deleteall()
  
  	local ReplicatedStorage = game:GetService("ReplicatedStorage")
  	local RequestCommand = ReplicatedStorage:WaitForChild("HDAdminHDClient").Signals.RequestCommandSilent
  	RequestCommand:InvokeServer(";fogcolor black ;time")
  	local player = game.Players.LocalPlayer
  	local char = player.Character
  	local backpack = player.Backpack
  
  	local function getf3x()
  		for _, v in ipairs(backpack:GetChildren()) do
  			if v:FindFirstChild("SyncAPI") then
  				return v
  			end
  		end
  		for _, v in ipairs(char:GetChildren()) do
  			if v:FindFirstChild("SyncAPI") then
  				return v
  			end
  		end
  
  		return nil
  	end
  	local f3x = getf3x()
  	if not f3x then
  		warn("you dont have f3x skid")
  	end
  	local syncapi = f3x.SyncAPI
  	local serverendpoint = syncapi.ServerEndpoint
  
  	local function resize(part,size,cf)
  		local args = {
  			[1] = "SyncResize",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["CFrame"] = cf,
  					["Size"] = size
  				}
  			}
  		}
  		serverendpoint:InvokeServer(unpack(args))
  	end
  
  	local function syncmaterial(part,mate,trans)
  		local args = {
  			[1] = "SyncMaterial",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["Material"] = mate
  				}
  			}
  		}
  		serverendpoint:InvokeServer(unpack(args))
  	end
  	local function transparency(part,trans)
  		local args = {
  			[1] = "SyncMaterial",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["Transparency"] = trans
  				}
  			}
  		}
  		serverendpoint:InvokeServer(unpack(args))
  	end
  
  	local function color(part, color)
  		local args = {
  			[1] = "SyncColor",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["Color"] = color --[[Color3]],
  					["UnionColoring"] = false
  				}
  			}
  		}
  		serverendpoint:InvokeServer(unpack(args))
  	end
  
  	local function syncmeshid(part, id)
  		local args = {
  			[1] = "SyncMesh",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["MeshId"] = "rbxassetid://"..id
  				}
  			}
  		}
  		serverendpoint:InvokeServer(unpack(args))
  	end
  
  	local function makemesh(part)
  		local args = {
  			[1] = "CreateMeshes",
  			[2] = {
  				[1] = {
  					["Part"] = part
  				}
  			}
  		}
  		serverendpoint:InvokeServer(unpack(args))
  	end
  
  	local function syncmeshsize(part, vectora)
  		local args = {
  			[1] = "SyncMesh",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["Scale"] = vectora
  				}
  			}
  		}
  		serverendpoint:InvokeServer(unpack(args))
  	end
  
  	local function syncmeshtexture(part, id)
  		local args = {
  			[1] = "SyncMesh",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["TextureId"] =	"rbxassetid://"..id
  				}
  			}
  		}
  		serverendpoint:InvokeServer(unpack(args))
  	end
  
  	local function name(part, stringa)
  		local args = {
  			[1] = "SetName",
  			[2] = {
  				[1] = part
  			},
  			[3] = stringa
  		}
  		serverendpoint:InvokeServer(unpack(args))
  	end
  
  	local function lock(part, boolean)
  		local args = {
  			[1] = "SetLocked",
  			[2] = {
  				[1] = part
  			},
  			[3] = boolean
  		}
  		serverendpoint:InvokeServer(unpack(args))
  	end
  
  	local function setcollision(part, booleana)
  		local args = {
  			[1] = "SyncCollision",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["CanCollide"] = booleana
  				}
  			}
  		}
  		serverendpoint:InvokeServer(unpack(args))
  	end
  
  	local function setanchor(part, boolean)
  		local args = {
  			[1] = "SyncAnchor",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["Anchored"] = boolean
  				}
  			}
  		}
  		serverendpoint:InvokeServer(unpack(args))
  	end
  
  	local function createdecal(part, side)
  		local args = {
  			[1] = "CreateTextures",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["Face"] = side,
  					["TextureType"] = "Decal"
  				}
  			}
  		}
  		serverendpoint:InvokeServer(unpack(args))
  	end
  	local function setdecal(part, asset, side)
  		local args = {
  			[1] = "SyncTexture",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["Face"] = side,
  					["TextureType"] = "Decal",
  					["Texture"] = "rbxassetid://".. asset
  				}
  			}
  		}
  		serverendpoint:InvokeServer(unpack(args))
  	end
  
  	local function makerealmbase()
  		local position = CFrame.new(0, 5, 0)
  		local base = serverendpoint:InvokeServer("CreatePart", "Normal", position, workspace)
  		resize(base, Vector3.new(512, 16, 512), position)
  		syncmaterial(base, Enum.Material.Concrete)
  		color(base, Color3.new(0.513725, 0.513725, 0.513725))
  		name(base, "loltroll")
  		lock(base, true)
  
  		local spawnpos = CFrame.new(34.5, 8.1, -26)
  		local spawna = serverendpoint:InvokeServer("CreatePart", "Spawn", spawnpos, workspace)
  		resize(spawna, Vector3.new(20, 10, 20), spawnpos)
  		name(spawna, "SpawnLocation")
  		lock(spawna, true)
  
  		createdecal(spawna, Enum.NormalId.Top)
  		setdecal(spawna, "ID", Enum.NormalId.Top) -- ganti decalnya pake decal lu
  		transparency(spawna, 1)
  
  		local pos = CFrame.new(74.143, 24, -25.232)
  
  		local rules = serverendpoint:InvokeServer("CreatePart", "Normal", pos, workspace)
  
  		transparency(rules, 0)
  		setcollision(rules, false)
  		createdecal(rules, Enum.NormalId.Left)
  		setdecal(rules, "ID", Enum.NormalId.Left)
  		color(rules, Color3.new(1, 1, 1))
  		resize(rules, Vector3.new(4, 23, 37), pos)
  
  
  		local pos = CFrame.new(1.143, 24, -25.232)
  
  		local bad = serverendpoint:InvokeServer("CreatePart", "Normal", pos, workspace)
  
  		transparency(bad, 1)
  		setcollision(bad, false)
  		createdecal(bad, Enum.NormalId.Right)
  		setdecal(bad, "ID", Enum.NormalId.Right)
  		resize(bad, Vector3.new(4, 23, 37), pos)
  
  	end
  
  	local function sky()
  		local position = CFrame.new(0, 5, 0)
  		local sky = serverendpoint:InvokeServer("CreatePart", "Normal", position, workspace)
  
  		makemesh(sky)
  		syncmeshid(sky, "111891702759441")
  		syncmeshtexture(sky, "ID")
  		syncmeshsize(sky, Vector3.new(99999, 99999, 99999))
  		lock(sky, true)
  		name(sky, "YOU NAME")
  		setcollision(sky, false)
  	end
  
  
  
  
  
  	local function unanchorall()
  		for _, v in ipairs(workspace:GetDescendants()) do
  			if v:IsA("BasePart") or v:IsA("UnionOperation") then
  				spawn(function()
  					setanchor(v, false)
  				end)
  			end
  		end
  	end
  
  	local function realm()
  		sky()
  		makerealmbase()
  	end
  
  	realm()
  
  	RequestCommand:InvokeServer(";res all")
  `,
    "spin-all": `
  local ReplicatedStorage = game:GetService("ReplicatedStorage")
  	local RequestCommand = ReplicatedStorage:WaitForChild("HDAdminHDClient").Signals.RequestCommandSilent
  
  	RequestCommand:InvokeServer(";spin all")
  `,
    "fire-parts": `
  local player = game.Players.LocalPlayer
  	local char = player.Character
  	local tool
  	for i,v in player:GetDescendants() do
  		if v.Name == "SyncAPI" then
  			tool = v.Parent
  		end
  	end
  	for i,v in game.ReplicatedStorage:GetDescendants() do
  		if v.Name == "SyncAPI" then
  			tool = v.Parent
  		end
  	end
  	--craaa
  	remote = tool.SyncAPI.ServerEndpoint
  	function _(args)
  		remote:InvokeServer(unpack(args))
  	end
  	function SetCollision(part,boolean)
  		local args = {
  			[1] = "SyncCollision",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["CanCollide"] = boolean
  				}
  			}
  		}
  		_(args)
  	end
  	function SetAnchor(boolean,part)
  		local args = {
  			[1] = "SyncAnchor",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["Anchored"] = boolean
  				}
  			}
  		}
  		_(args)
  	end
  	function CreatePart(cf,parent)
  		local args = {
  			[1] = "CreatePart",
  			[2] = "Normal",
  			[3] = cf,
  			[4] = parent
  		}
  		_(args)
  	end
  	function DestroyPart(part)
  		local args = {
  			[1] = "Remove",
  			[2] = {
  				[1] = part
  			}
  		}
  		_(args)
  	end
  	function MovePart(part,cf)
  		local args = {
  			[1] = "SyncMove",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["CFrame"] = cf
  				}
  			}
  		}
  		_(args)
  	end
  	function Resize(part,size,cf)
  		local args = {
  			[1] = "SyncResize",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["CFrame"] = cf,
  					["Size"] = size
  				}
  			}
  		}
  		_(args)
  	end
  	function AddMesh(part)
  		local args = {
  			[1] = "CreateMeshes",
  			[2] = {
  				[1] = {
  					["Part"] = part
  				}
  			}
  		}
  		_(args)
  	end
  
  	function SetMesh(part,meshid)
  		local args = {
  			[1] = "SyncMesh",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["MeshId"] = "rbxassetid://"..meshid
  				}
  			}
  		}
  		_(args)
  	end
  	function SetTexture(part, texid)
  		local args = {
  			[1] = "SyncMesh",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["TextureId"] = "rbxassetid://"..texid
  				}
  			}
  		}
  		_(args)
  	end
  	function SetName(part, stringg)
  		local args = {
  			[1] = "SetName",
  			[2] = {
  				[1] = workspace.Part
  			},
  			[3] = stringg
  		}
  
  		_(args)
  	end
  	function MeshResize(part,size)
  		local args = {
  			[1] = "SyncMesh",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["Scale"] = size
  				}
  			}
  		}
  		_(args)
  	end
  	function Weld(part1, part2,lead)
  		local args = {
  			[1] = "CreateWelds",
  			[2] = {
  				[1] = part1,
  				[2] = part2
  			},
  			[3] = lead
  		}
  		_(args)
  
  	end
  	function SetLocked(part,boolean)
  		local args = {
  			[1] = "SetLocked",
  			[2] = {
  				[1] = part
  			},
  			[3] = boolean
  		}
  		_(args)
  	end
  	function SetTrans(part,int)
  		local args = {
  			[1] = "SyncMaterial",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["Transparency"] = int
  				}
  			}
  		}
  		_(args)
  	end
  	function CreateSpotlight(part)
  		local args = {
  			[1] = "CreateLights",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["LightType"] = "SpotLight"
  				}
  			}
  		}
  		_(args)
  	end
  	function SyncLighting(part,brightness)
  		local args = {
  			[1] = "SyncLighting",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["LightType"] = "SpotLight",
  					["Brightness"] = brightness
  				}
  			}
  		}
  		_(args)
  	end
  	function AddFire(part)
  		local args = {
  			[1] = "CreateDecorations",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["DecorationType"] = "Fire"
  				}
  			}
  		}
  		_(args)
  	end
  	function FireParts()
  		for i,v in game.Workspace:GetDescendants() do
  			spawn(function()
  				SetLocked(v,false)
  				AddFire(v)
  			end)
  		end
  	end
  	FireParts()
  `,
    "mario.exe": `
  local ReplicatedStorage = game:GetService("ReplicatedStorage")
  	local RequestCommand = ReplicatedStorage:WaitForChild("HDAdminHDClient").Signals.RequestCommandSilent
  
  	RequestCommand:InvokeServer(";music 133180219581309")
  	RequestCommand:InvokeServer(";pitch 0.11")
  	RequestCommand:InvokeServer(";volume inf")
  	
  	local player = game.Players.LocalPlayer
  	local char = player.Character
  	local tool
  	for i,v in player:GetDescendants() do
  		if v.Name == "SyncAPI" then
  			tool = v.Parent
  		end
  	end
  	for i,v in game.ReplicatedStorage:GetDescendants() do
  		if v.Name == "SyncAPI" then
  			tool = v.Parent
  		end
  	end
  	--craaa
  	remote = tool.SyncAPI.ServerEndpoint
  	function _(args)
  		remote:InvokeServer(unpack(args))
  	end
  	function SetCollision(part,boolean)
  		local args = {
  			[1] = "SyncCollision",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["CanCollide"] = boolean
  				}
  			}
  		}
  		_(args)
  	end
  	function SetAnchor(boolean,part)
  		local args = {
  			[1] = "SyncAnchor",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["Anchored"] = boolean
  				}
  			}
  		}
  		_(args)
  	end
  	function CreatePart(cf,parent)
  		local args = {
  			[1] = "CreatePart",
  			[2] = "Normal",
  			[3] = cf,
  			[4] = parent
  		}
  		_(args)
  	end
  	function DestroyPart(part)
  		local args = {
  			[1] = "Remove",
  			[2] = {
  				[1] = part
  			}
  		}
  		_(args)
  	end
  	function MovePart(part,cf)
  		local args = {
  			[1] = "SyncMove",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["CFrame"] = cf
  				}
  			}
  		}
  		_(args)
  	end
  	function Resize(part,size,cf)
  		local args = {
  			[1] = "SyncResize",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["CFrame"] = cf,
  					["Size"] = size
  				}
  			}
  		}
  		_(args)
  	end
  	function AddMesh(part)
  		local args = {
  			[1] = "CreateMeshes",
  			[2] = {
  				[1] = {
  					["Part"] = part
  				}
  			}
  		}
  		_(args)
  	end
  
  	function SetMesh(part,meshid)
  		local args = {
  			[1] = "SyncMesh",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["MeshId"] = "rbxassetid://"..meshid
  				}
  			}
  		}
  		_(args)
  	end
  	function SetTexture(part, texid)
  		local args = {
  			[1] = "SyncMesh",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["TextureId"] = "rbxassetid://"..texid
  				}
  			}
  		}
  		_(args)
  	end
  	function SetName(part, stringg)
  		local args = {
  			[1] = "SetName",
  			[2] = {
  				[1] = part
  			},
  			[3] = stringg
  		}
  
  		_(args)
  	end
  	function MeshResize(part,size)
  		local args = {
  			[1] = "SyncMesh",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["Scale"] = size
  				}
  			}
  		}
  		_(args)
  	end
  	function Weld(part1, part2,lead)
  		local args = {
  			[1] = "CreateWelds",
  			[2] = {
  				[1] = part1,
  				[2] = part2
  			},
  			[3] = lead
  		}
  		_(args)
  
  	end
  	function SetLocked(part,boolean)
  		local args = {
  			[1] = "SetLocked",
  			[2] = {
  				[1] = part
  			},
  			[3] = boolean
  		}
  		_(args)
  	end
  	function SetTrans(part,int)
  		local args = {
  			[1] = "SyncMaterial",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["Transparency"] = int
  				}
  			}
  		}
  		_(args)
  	end
  	function CreateSpotlight(part)
  		local args = {
  			[1] = "CreateLights",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["LightType"] = "SpotLight"
  				}
  			}
  		}
  		_(args)
  	end
  	function SyncLighting(part,brightness)
  		local args = {
  			[1] = "SyncLighting",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["LightType"] = "SpotLight",
  					["Brightness"] = brightness
  				}
  			}
  		}
  		_(args)
  	end
  	function Color(part,color)
  		local args = {
  			[1] = "SyncColor",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["Color"] = color --[[Color3]],
  					["UnionColoring"] = false
  				}
  			}
  		}
  		_(args)
  	end
  	function SpawnDecal(part,side)
  		local args = {
  			[1] = "CreateTextures",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["Face"] = side,
  					["TextureType"] = "Decal"
  				}
  			}
  		}
  
  		_(args)
  	end
  	function AddDecal(part,asset,side)
  		local args = {
  			[1] = "SyncTexture",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["Face"] = side,
  					["TextureType"] = "Decal",
  					["Texture"] = "rbxassetid://".. asset
  				}
  			}
  		}
  		_(args)
  	end
  
  	function spam(id)
  		for i,v in game.workspace:GetDescendants() do
  			if v:IsA("BasePart") then
  				spawn(function()
  					SetLocked(v,false)
  					SpawnDecal(v,Enum.NormalId.Front)
  					AddDecal(v,id,Enum.NormalId.Front)
  
  					SpawnDecal(v,Enum.NormalId.Back)
  					AddDecal(v,id,Enum.NormalId.Back)
  
  					SpawnDecal(v,Enum.NormalId.Right)
  					AddDecal(v,id,Enum.NormalId.Right)
  
  					SpawnDecal(v,Enum.NormalId.Left)
  					AddDecal(v,id,Enum.NormalId.Left)
  
  					SpawnDecal(v,Enum.NormalId.Bottom)
  					AddDecal(v,id,Enum.NormalId.Bottom)
  
  					SpawnDecal(v,Enum.NormalId.Top)
  					AddDecal(v,id,Enum.NormalId.Top)
  				end)
  			end
  		end 
  	end
  	spam("137939198058148")
  	
  	local ReplicatedStorage = game:GetService("ReplicatedStorage")
  	local RequestCommand = ReplicatedStorage:WaitForChild("HDAdminHDClient").Signals.RequestCommandSilent
  
  	RequestCommand:InvokeServer(";time 17")
  	
  	wait (1)
  	
  	local player = game.Players.LocalPlayer
  	local char = player.Character
  	local tool
  	for i,v in player:GetDescendants() do
  		if v.Name == "SyncAPI" then
  			tool = v.Parent
  		end
  	end
  	for i,v in game.ReplicatedStorage:GetDescendants() do
  		if v.Name == "SyncAPI" then
  			tool = v.Parent
  		end
  	end
  	--craaa
  	remote = tool.SyncAPI.ServerEndpoint
  	function _(args)
  		remote:InvokeServer(unpack(args))
  	end
  	function SetCollision(part,boolean)
  		local args = {
  			[1] = "SyncCollision",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["CanCollide"] = boolean
  				}
  			}
  		}
  		_(args)
  	end
  	function SetAnchor(boolean,part)
  		local args = {
  			[1] = "SyncAnchor",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["Anchored"] = boolean
  				}
  			}
  		}
  		_(args)
  	end
  	function CreatePart(cf,parent)
  		local args = {
  			[1] = "CreatePart",
  			[2] = "Normal",
  			[3] = cf,
  			[4] = parent
  		}
  		_(args)
  	end
  	function DestroyPart(part)
  		local args = {
  			[1] = "Remove",
  			[2] = {
  				[1] = part
  			}
  		}
  		_(args)
  	end
  	function MovePart(part,cf)
  		local args = {
  			[1] = "SyncMove",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["CFrame"] = cf
  				}
  			}
  		}
  		_(args)
  	end
  	function Resize(part,size,cf)
  		local args = {
  			[1] = "SyncResize",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["CFrame"] = cf,
  					["Size"] = size
  				}
  			}
  		}
  		_(args)
  	end
  	function AddMesh(part)
  		local args = {
  			[1] = "CreateMeshes",
  			[2] = {
  				[1] = {
  					["Part"] = part
  				}
  			}
  		}
  		_(args)
  	end
  
  	function SetMesh(part,meshid)
  		local args = {
  			[1] = "SyncMesh",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["MeshId"] = "rbxassetid://"..meshid
  				}
  			}
  		}
  		_(args)
  	end
  	function SetTexture(part, texid)
  		local args = {
  			[1] = "SyncMesh",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["TextureId"] = "rbxassetid://"..texid
  				}
  			}
  		}
  		_(args)
  	end
  	function SetName(part, stringg)
  		local args = {
  			[1] = "SetName",
  			[2] = {
  				[1] = part
  			},
  			[3] = stringg
  		}
  
  		_(args)
  	end
  	function MeshResize(part,size)
  		local args = {
  			[1] = "SyncMesh",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["Scale"] = size
  				}
  			}
  		}
  		_(args)
  	end
  	function Weld(part1, part2,lead)
  		local args = {
  			[1] = "CreateWelds",
  			[2] = {
  				[1] = part1,
  				[2] = part2
  			},
  			[3] = lead
  		}
  		_(args)
  
  	end
  	function SetLocked(part,boolean)
  		local args = {
  			[1] = "SetLocked",
  			[2] = {
  				[1] = part
  			},
  			[3] = boolean
  		}
  		_(args)
  	end
  	function SetTrans(part,int)
  		local args = {
  			[1] = "SyncMaterial",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["Transparency"] = int
  				}
  			}
  		}
  		_(args)
  	end
  	function CreateSpotlight(part)
  		local args = {
  			[1] = "CreateLights",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["LightType"] = "SpotLight"
  				}
  			}
  		}
  		_(args)
  	end
  	function SyncLighting(part,brightness)
  		local args = {
  			[1] = "SyncLighting",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["LightType"] = "SpotLight",
  					["Brightness"] = brightness
  				}
  			}
  		}
  		_(args)
  	end
  	function Color(part,color)
  		local args = {
  			[1] = "SyncColor",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["Color"] = color --[[Color3]],
  					["UnionColoring"] = false
  				}
  			}
  		}
  		_(args)
  	end
  	function SpawnDecal(part,side)
  		local args = {
  			[1] = "CreateTextures",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["Face"] = side,
  					["TextureType"] = "Decal"
  				}
  			}
  		}
  
  		_(args)
  	end
  	function AddDecal(part,asset,side)
  		local args = {
  			[1] = "SyncTexture",
  			[2] = {
  				[1] = {
  					["Part"] = part,
  					["Face"] = side,
  					["TextureType"] = "Decal",
  					["Texture"] = "rbxassetid://".. asset
  				}
  			}
  		}
  		_(args)
  	end
  
  	function Sky(id)
  		e = char.HumanoidRootPart.CFrame.x
  		f = char.HumanoidRootPart.CFrame.y
  		g = char.HumanoidRootPart.CFrame.z
  		CreatePart(CFrame.new(math.floor(e),math.floor(f),math.floor(g)) + Vector3.new(0,6,0),workspace)
  		for i,v in game.Workspace:GetDescendants() do
  			if v:IsA("BasePart") and v.CFrame.x == math.floor(e) and v.CFrame.z == math.floor(g) then
  				--spawn(function()
  				SetName(v,"Sky")
  				AddMesh(v)
  				--end)
  				--spawn(function()
  				SetMesh(v,"111891702759441")
  				SetTexture(v,id)
  				--end)
  				MeshResize(v,Vector3.new(99999,99999,99999))
  				SetLocked(v,true)
  			end
  		end
  	end
  	Sky("137939198058148")
  	
  	wait (0.5)
  	
  	local ReplicatedStorage = game:GetService("ReplicatedStorage")
  	local RequestCommand = ReplicatedStorage:WaitForChild("HDAdminHDClient").Signals.RequestCommandSilent
  
  	RequestCommand:InvokeServer(";fogcolor black")
  `,
    "baseplate": `
  local player = game.Players.LocalPlayer
  
  	local char = player.Character
  
  	local tool
  
  	for i,v in player:GetDescendants() do
  
  		if v.Name == "SyncAPI" then
  
  			tool = v.Parent
  
  		end
  
  	end
  
  	for i,v in game.ReplicatedStorage:GetDescendants() do
  
  		if v.Name == "SyncAPI" then
  
  			tool = v.Parent
  
  		end
  
  	end
  
  	--craaa
  
  	remote = tool.SyncAPI.ServerEndpoint
  
  	function _(args)
  
  		remote:InvokeServer(unpack(args))
  
  	end
  
  	function SetCollision(part,boolean)
  
  		local args = {
  
  			[1] = "SyncCollision",
  
  			[2] = {
  
  				[1] = {
  
  					["Part"] = part,
  
  					["CanCollide"] = boolean
  
  				}
  
  			}
  
  		}
  
  		_(args)
  
  	end
  
  	function SetAnchor(boolean,part)
  
  		local args = {
  
  			[1] = "SyncAnchor",
  
  			[2] = {
  
  				[1] = {
  
  					["Part"] = part,
  
  					["Anchored"] = boolean
  
  				}
  
  			}
  
  		}
  
  		_(args)
  
  	end
  
  	function CreatePart(cf,parent,types)
  
  		local args = {
  
  			[1] = "CreatePart",
  
  			[2] = types,
  
  			[3] = cf,
  
  			[4] = parent
  
  		}
  
  		_(args)
  
  	end
  
  	function DestroyPart(part)
  
  		local args = {
  
  			[1] = "Remove",
  
  			[2] = {
  
  				[1] = part
  
  			}
  
  		}
  
  		_(args)
  
  	end
  
  	function MovePart(part,cf)
  
  		local args = {
  
  			[1] = "SyncMove",
  
  			[2] = {
  
  				[1] = {
  
  					["Part"] = part,
  
  					["CFrame"] = cf
  
  				}
  
  			}
  
  		}
  
  		_(args)
  
  	end
  
  	function Resize(part,size,cf)
  
  		local args = {
  
  			[1] = "SyncResize",
  
  			[2] = {
  
  				[1] = {
  
  					["Part"] = part,
  
  					["CFrame"] = cf,
  
  					["Size"] = size
  
  				}
  
  			}
  
  		}
  
  		_(args)
  
  	end
  
  	function AddMesh(part)
  
  		local args = {
  
  			[1] = "CreateMeshes",
  
  			[2] = {
  
  				[1] = {
  
  					["Part"] = part
  
  				}
  
  			}
  
  		}
  
  		_(args)
  
  	end
  
  	function SetMesh(part,meshid)
  
  		local args = {
  
  			[1] = "SyncMesh",
  
  			[2] = {
  
  				[1] = {
  
  					["Part"] = part,
  
  					["MeshId"] = "rbxassetid://"..meshid
  
  				}
  
  			}
  
  		}
  
  		_(args)
  
  	end
  
  	function SetTexture(part, texid)
  
  		local args = {
  
  			[1] = "SyncMesh",
  
  			[2] = {
  
  				[1] = {
  
  					["Part"] = part,
  
  					["TextureId"] = "rbxassetid://"..texid
  
  				}
  
  			}
  
  		}
  
  		_(args)
  
  	end
  
  	function SetName(part, stringg)
  
  		local args = {
  
  			[1] = "SetName",
  
  			[2] = {
  
  				[1] = workspace.Part
  
  			},
  
  			[3] = stringg
  
  		}
  
  		_(args)
  
  	end
  
  	function MeshResize(part,size)
  
  		local args = {
  
  			[1] = "SyncMesh",
  
  			[2] = {
  
  				[1] = {
  
  					["Part"] = part,
  
  					["Scale"] = size
  
  				}
  
  			}
  
  		}
  
  		_(args)
  
  	end
  
  	function Weld(part1, part2,lead)
  
  		local args = {
  
  			[1] = "CreateWelds",
  
  			[2] = {
  
  				[1] = part1,
  
  				[2] = part2
  
  			},
  
  			[3] = lead
  
  		}
  
  		_(args)
  
  	end
  
  	function SetLocked(part,boolean)
  
  		local args = {
  
  			[1] = "SetLocked",
  
  			[2] = {
  
  				[1] = part
  
  			},
  
  			[3] = boolean
  
  		}
  
  		_(args)
  
  	end
  
  	function SetTrans(part,int)
  
  		local args = {
  
  			[1] = "SyncMaterial",
  
  			[2] = {
  
  				[1] = {
  
  					["Part"] = part,
  
  					["Transparency"] = int
  
  				}
  
  			}
  
  		}
  
  		_(args)
  
  	end
  
  	function CreateSpotlight(part)
  
  		local args = {
  
  			[1] = "CreateLights",
  
  			[2] = {
  
  				[1] = {
  
  					["Part"] = part,
  
  					["LightType"] = "SpotLight"
  
  				}
  
  			}
  
  		}
  
  		_(args)
  
  	end
  
  	function SyncLighting(part,brightness)
  
  		local args = {
  
  			[1] = "SyncLighting",
  
  			[2] = {
  
  				[1] = {
  
  					["Part"] = part,
  
  					["LightType"] = "SpotLight",
  
  					["Brightness"] = brightness
  
  				}
  
  			}
  
  		}
  
  		_(args)
  
  	end
  
  	function Material(part,mate)
  
  		local args = {
  
  			[1] = "SyncMaterial",
  
  			[2] = {
  
  				[1] = {
  
  					["Part"] = part,
  
  					["Material"] = mate
  
  				}
  
  			}
  
  		}
  
  		_(args)
  
  	end
  
  	function Color(part,color)
  
  		local args = {
  
  			[1] = "SyncColor",
  
  			[2] = {
  
  				[1] = {
  
  					["Part"] = part,
  
  					["Color"] = color --[[Color3]],
  
  					["UnionColoring"] = false
  
  				}
  
  			}
  
  		}
  
  		_(args)
  
  	end
  
  	function toptexturecreate(part)
  
  		local args = {
  
  			[1] = "CreateTextures",
  
  			[2] = {
  
  				[1] = {
  
  					["Part"] = part,
  
  					["Face"] = Enum.NormalId.Top,
  
  					["TextureType"] = "Texture"
  
  				}
  
  			}
  
  		}
  
  		_(args)
  
  	end
  
  	function toptextureadd(part)
  
  		local args = {
  
  			[1] = "SyncTexture",
  
  			[2] = {
  
  				[1] = {
  
  					["Part"] = part,
  
  					["Face"] = Enum.NormalId.Top,
  
  					["TextureType"] = "Texture",
  
  					["Texture"] = "rbxassetid://ID",
  
  					["StudsPerTileV"] = 20,
  
  					["StudsPerTileU"] = 20
  
  				}
  
  			}
  
  		}
  
  		_(args)
  
  	end
  
  	hrpx = math.floor(char.HumanoidRootPart.CFrame.x)
  
  	hrpz = math.floor(char.HumanoidRootPart.CFrame.z)
  
  	hrpy = math.floor(char.HumanoidRootPart.CFrame.y)
  
  	function baseplate()
  
  		CreatePart(CFrame.new(hrpx,hrpy-20,hrpz),workspace,"Spawn")
  
  		for i,v in game.Workspace:GetChildren() do
  
  			if v:IsA("BasePart") and v.CFrame.y == hrpy - 20 and v.CFrame.x == hrpx then
  
  				spawn(function()
  
  					Resize(v,Vector3.new(1000,2,1000),CFrame.new(hrpx,hrpy-20,hrpz))
  
  					Color(v,Color3.fromRGB(0,0,0))
  
  					toptexturecreate(v)
  
  					toptextureadd(v)
  
  					while wait(1) do
  
  						pcall(function()SetLocked(v,true)end)
  
  					end
  
  				end)
  
  			end
  
  		end
  
  	end
  
  	baseplate()
  `,
    "unanchor": `
  local player = game.Players.LocalPlayer
  
  	local char = player.Character
  
  	local tool
  
  	for i,v in player:GetDescendants() do
  
  		if v.Name == "SyncAPI" then
  
  			tool = v.Parent
  
  		end
  
  	end
  
  	for i,v in game.ReplicatedStorage:GetDescendants() do
  
  		if v.Name == "SyncAPI" then
  
  			tool = v.Parent
  
  		end
  
  	end
  
  	--craaa
  
  	remote = tool.SyncAPI.ServerEndpoint
  
  	function _(args)
  
  		remote:InvokeServer(unpack(args))
  
  	end
  
  	function SetCollision(part,boolean)
  
  		local args = {
  
  			[1] = "SyncCollision",
  
  			[2] = {
  
  				[1] = {
  
  					["Part"] = part,
  
  					["CanCollide"] = boolean
  
  				}
  
  			}
  
  		}
  
  		_(args)
  
  	end
  
  	function SetAnchor(boolean,part)
  
  		local args = {
  
  			[1] = "SyncAnchor",
  
  			[2] = {
  
  				[1] = {
  
  					["Part"] = part,
  
  					["Anchored"] = boolean
  
  				}
  
  			}
  
  		}
  
  		_(args)
  
  	end
  
  	function CreatePart(cf,parent)
  
  		local args = {
  
  			[1] = "CreatePart",
  
  			[2] = "Normal",
  
  			[3] = cf,
  
  			[4] = parent
  
  		}
  
  		_(args)
  
  	end
  
  	function DestroyPart(part)
  
  		local args = {
  
  			[1] = "Remove",
  
  			[2] = {
  
  				[1] = part
  
  			}
  
  		}
  
  		_(args)
  
  	end
  
  	function MovePart(part,cf)
  
  		local args = {
  
  			[1] = "SyncMove",
  
  			[2] = {
  
  				[1] = {
  
  					["Part"] = part,
  
  					["CFrame"] = cf
  
  				}
  
  			}
  
  		}
  
  		_(args)
  
  	end
  
  	function Resize(part,size,cf)
  
  		local args = {
  
  			[1] = "SyncResize",
  
  			[2] = {
  
  				[1] = {
  
  					["Part"] = part,
  
  					["CFrame"] = cf,
  
  					["Size"] = size
  
  				}
  
  			}
  
  		}
  
  		_(args)
  
  	end
  
  	function AddMesh(part)
  
  		local args = {
  
  			[1] = "CreateMeshes",
  
  			[2] = {
  
  				[1] = {
  
  					["Part"] = part
  
  				}
  
  			}
  
  		}
  
  		_(args)
  
  	end
  
  	function SetMesh(part,meshid)
  
  		local args = {
  
  			[1] = "SyncMesh",
  
  			[2] = {
  
  				[1] = {
  
  					["Part"] = part,
  
  					["MeshId"] = "rbxassetid://"..meshid
  
  				}
  
  			}
  
  		}
  
  		_(args)
  
  	end
  
  	function SetTexture(part, texid)
  
  		local args = {
  
  			[1] = "SyncMesh",
  
  			[2] = {
  
  				[1] = {
  
  					["Part"] = part,
  
  					["TextureId"] = "rbxassetid://"..texid
  
  				}
  
  			}
  
  		}
  
  		_(args)
  
  	end
  
  	function SetName(part, stringg)
  
  		local args = {
  
  			[1] = "SetName",
  
  			[2] = {
  
  				[1] = workspace.Part
  
  			},
  
  			[3] = stringg
  
  		}
  
  		_(args)
  
  	end
  
  	function MeshResize(part,size)
  
  		local args = {
  
  			[1] = "SyncMesh",
  
  			[2] = {
  
  				[1] = {
  
  					["Part"] = part,
  
  					["Scale"] = size
  
  				}
  
  			}
  
  		}
  
  		_(args)
  
  	end
  
  	function Weld(part1, part2,lead)
  
  		local args = {
  
  			[1] = "CreateWelds",
  
  			[2] = {
  
  				[1] = part1,
  
  				[2] = part2
  
  			},
  
  			[3] = lead
  
  		}
  
  		_(args)
  
  	end
  
  	function SetLocked(part,boolean)
  
  		local args = {
  
  			[1] = "SetLocked",
  
  			[2] = {
  
  				[1] = part
  
  			},
  
  			[3] = boolean
  
  		}
  
  		_(args)
  
  	end
  
  	function SetTrans(part,int)
  
  		local args = {
  
  			[1] = "SyncMaterial",
  
  			[2] = {
  
  				[1] = {
  
  					["Part"] = part,
  
  					["Transparency"] = int
  
  				}
  
  			}
  
  		}
  
  		_(args)
  
  	end
  
  	function CreateSpotlight(part)
  
  		local args = {
  
  			[1] = "CreateLights",
  
  			[2] = {
  
  				[1] = {
  
  					["Part"] = part,
  
  					["LightType"] = "SpotLight"
  
  				}
  
  			}
  
  		}
  
  		_(args)
  
  	end
  
  	function SyncLighting(part,brightness)
  
  		local args = {
  
  			[1] = "SyncLighting",
  
  			[2] = {
  
  				[1] = {
  
  					["Part"] = part,
  
  					["LightType"] = "SpotLight",
  
  					["Brightness"] = brightness
  
  				}
  
  			}
  
  		}
  
  		_(args)
  
  	end
  
  	function Unanchor()
  
  		for i,v in game.Workspace:GetDescendants() do
  
  			spawn(function()
  
  				SetLocked(v,false)
  
  				SetAnchor(false,v)
  
  			end)
  
  		end
  
  	end
  
  	Unanchor()
  `,
    "skys": `
  --==[ SKY SPIN BY MO0PKIDD PLS DO NOT REMOVE THIS CREDIT ]==--
  local player = game.Players.LocalPlayer
  local char = player.Character or player.CharacterAdded:Wait()
  local tool
  
  for _,v in ipairs(player:GetDescendants()) do
  	if v.Name=="SyncAPI" then tool=v.Parent end
  end
  for _,v in ipairs(game.ReplicatedStorage:GetDescendants()) do
  	if v.Name=="SyncAPI" then tool=v.Parent end
  end
  if not tool then return warn("F3X / SyncAPI Not found") end
  
  local remote = tool.SyncAPI.ServerEndpoint
  local function _(args) remote:InvokeServer(unpack(args)) end
  
  local function SetLocked(p,b) _( {"SetLocked",{p},b} ) end
  local function SetAnchor(p,b) _( {"SyncAnchor",{{Part=p,Anchored=b}}} ) end
  local function SyncCollision(p,b) _( {"SyncCollision",{{Part=p,CanCollide=b}}} ) end
  local function CreatePart(cf,parent) _( {"CreatePart","Normal",cf,parent} ) end
  local function AddMesh(p) _( {"CreateMeshes",{{Part=p}}} ) end
  local function SetMesh(p,id) _( {"SyncMesh",{{Part=p,MeshId="rbxassetid://"..id}}} ) end
  local function SetTexture(p,id) _( {"SyncMesh",{{Part=p,TextureId=id}}} ) end
  local function MeshResize(p,scale) _( {"SyncMesh",{{Part=p,Scale=scale}}} ) end
  local function SpawnDecal(p,face) _( {"CreateTextures",{{Part=p,Face=face,TextureType="Decal"}}} ) end
  local function AddDecal(p,id,face) _( {"SyncTexture",{{Part=p,Face=face,TextureType="Decal",Texture=id}}} ) end
  
  local RS = game:GetService("RunService")
  
  skylol = setmetatable({},{
  	__index = function(t,id)
  		return function(size)
  			if not size then return warn("VocÃª precisa passar um Vector3 para o tamanho!") end
  
  			local root = char:WaitForChild("HumanoidRootPart")
  			local pos = root.Position + Vector3.new(0,6,0)
  
  			CreatePart(CFrame.new(pos), workspace)
  			task.wait(0.25)
  
  			local part
  			for _,v in ipairs(workspace:GetChildren()) do
  				if v:IsA("BasePart") and (v.Position-pos).Magnitude < 1 then
  					part = v
  					break
  				end
  			end
  			if not part then return end
  
  			SetLocked(part,true)
  			SetAnchor(part,true)
  			SyncCollision(part,false)
  
  			AddMesh(part)
  			SetMesh(part,"111891702759441")
  			SetTexture(part,id)
  			MeshResize(part,size)
  
  			for _,face in ipairs(Enum.NormalId:GetEnumItems()) do
  				SpawnDecal(part,face)
  				AddDecal(part,id,face)
  			end
  
  			local baseCF = part.CFrame
  			local ang = 0
  
  			RS.Heartbeat:Connect(function(dt)
  				if part and part.Parent then
  					ang += math.rad(35) * dt
  					local cf = baseCF * CFrame.Angles(ang, ang, ang)
  					_({"SyncRotate",{{Part=part,CFrame=cf}}})
  					part.CFrame = cf
  				end
  			end)
  		end
  	end
  })
  
  skylol["rbxassetid://YOUR ID"](Vector3.new(11000,11000,11000))
  `,
    "skyw": `
  local player = game.Players.LocalPlayer
  		local char = player.Character
  		local backpack = player.Backpack
  	
  		local function getf3x()
  			for _, v in ipairs(backpack:GetChildren()) do
  				if v:FindFirstChild("SyncAPI") then
  					return v
  				end
  			end
  			for _, v in ipairs(char:GetChildren()) do
  				if v:FindFirstChild("SyncAPI") then
  					return v
  				end
  			end
  	
  			return nil
  		end
  	
  		-- get all info
  	
  		local f3x = getf3x()
  		if not f3x then
  			warn("you dont have f3x skid")
  		end
  		local syncapi = f3x.SyncAPI
  		local serverendpoint = syncapi.ServerEndpoint
  	
  		-- name func
  	
  		local function name(part, stringa)
  			local args = {
  				[1] = "SetName",
  				[2] = {
  					[1] = part
  				},
  				[3] = stringa
  			}
  			serverendpoint:InvokeServer(unpack(args))
  		end
  		
  		local function setcollision(part, booleana)
  			local args = {
  				[1] = "SyncCollision",
  				[2] = {
  					[1] = {
  						["Part"] = part,
  						["CanCollide"] = booleana
  					}
  				}
  			}
  			serverendpoint:InvokeServer(unpack(args))
  		end
  	
  		local function lock(part, boolean)
  			local args = {
  				[1] = "SetLocked",
  				[2] = {
  					[1] = part
  				},
  				[3] = boolean
  			}
  			serverendpoint:InvokeServer(unpack(args))
  		end
  	
  		-- sky func
  	
  		local function sky()
  			spawn(function()
  				local position = char.Head.Position
  				local part = serverendpoint:InvokeServer("CreatePart", "Normal", CFrame.new(position + Vector3.new(0, 2, 0)), workspace)
  				local args = {
  					[1] = "CreateMeshes",
  					[2] = {
  						[1] = {
  							["Part"] = part
  						}
  					}
  				}
  				serverendpoint:InvokeServer(unpack(args))
  				local args = {
  					[1] = "SyncMesh",
  					[2] = {
  						[1] = {
  							["Part"] = part,
  							["MeshId"] = "rbxassetid://8006679977"
  						}
  					}
  				}
  				serverendpoint:InvokeServer(unpack(args))
  				local args = {
  					[1] = "SyncMesh",
  					[2] = {
  						[1] = {
  							["Part"] = part,
  							["Scale"] = Vector3.new(900, 900, 900)
  						}
  					}
  				}
  				serverendpoint:InvokeServer(unpack(args))
  				local args = {
  					[1] = "SyncMesh",
  					[2] = {
  						[1] = {
  							["Part"] = part,
  							["TextureId"] =	"rbxassetid://ID"
  						}
  					}
  				}
  				serverendpoint:InvokeServer(unpack(args))
  	
  				name(part, "Sky")
  				lock(part, true)
  				setcollision(part, false)
  			end)
  		end
  	
  		sky()
  
  
  local ReplicatedStorage = game:GetService("ReplicatedStorage")
  	local RequestCommand = ReplicatedStorage:WaitForChild("HDAdminHDClient").Signals.RequestCommandSilent
  
  	RequestCommand:InvokeServer(";time 0")
  
  local ReplicatedStorage = game:GetService("ReplicatedStorage")
  	local RequestCommand = ReplicatedStorage:WaitForChild("HDAdminHDClient").Signals.RequestCommandSilent
  
  	RequestCommand:InvokeServer(";time 12")
  
  
  local ReplicatedStorage = game:GetService("ReplicatedStorage")
  	local RequestCommand = ReplicatedStorage:WaitForChild("HDAdminHDClient").Signals.RequestCommandSilent
  
  	RequestCommand:InvokeServer(";time 0")
  
  local ReplicatedStorage = game:GetService("ReplicatedStorage")
  	local RequestCommand = ReplicatedStorage:WaitForChild("HDAdminHDClient").Signals.RequestCommandSilent
  
  	RequestCommand:InvokeServer(";time 0")
  
  local ReplicatedStorage = game:GetService("ReplicatedStorage")
  	local RequestCommand = ReplicatedStorage:WaitForChild("HDAdminHDClient").Signals.RequestCommandSilent
  
  	RequestCommand:InvokeServer(";time 12")
  
  
  local ReplicatedStorage = game:GetService("ReplicatedStorage")
  	local RequestCommand = ReplicatedStorage:WaitForChild("HDAdminHDClient").Signals.RequestCommandSilent
  
  	RequestCommand:InvokeServer(";time 0")
  
  local ReplicatedStorage = game:GetService("ReplicatedStorage")
  	local RequestCommand = ReplicatedStorage:WaitForChild("HDAdminHDClient").Signals.RequestCommandSilent
  
  	RequestCommand:InvokeServer(";time 0")
  
  local ReplicatedStorage = game:GetService("ReplicatedStorage")
  	local RequestCommand = ReplicatedStorage:WaitForChild("HDAdminHDClient").Signals.RequestCommandSilent
  
  	RequestCommand:InvokeServer(";time 12")
  
  
  local ReplicatedStorage = game:GetService("ReplicatedStorage")
  	local RequestCommand = ReplicatedStorage:WaitForChild("HDAdminHDClient").Signals.RequestCommandSilent
  
  	RequestCommand:InvokeServer(";time 0")
  
  local ReplicatedStorage = game:GetService("ReplicatedStorage")
  	local RequestCommand = ReplicatedStorage:WaitForChild("HDAdminHDClient").Signals.RequestCommandSilent
  
  	RequestCommand:InvokeServer(";time 0")
  
  local ReplicatedStorage = game:GetService("ReplicatedStorage")
  	local RequestCommand = ReplicatedStorage:WaitForChild("HDAdminHDClient").Signals.RequestCommandSilent
  
  	RequestCommand:InvokeServer(";time 12")
  
  
  local ReplicatedStorage = game:GetService("ReplicatedStorage")
  	local RequestCommand = ReplicatedStorage:WaitForChild("HDAdminHDClient").Signals.RequestCommandSilent
  
  	RequestCommand:InvokeServer(";time 0")
  
  local ReplicatedStorage = game:GetService("ReplicatedStorage")
  	local RequestCommand = ReplicatedStorage:WaitForChild("HDAdminHDClient").Signals.RequestCommandSilent
  
  	RequestCommand:InvokeServer(";time 0")
  
  local ReplicatedStorage = game:GetService("ReplicatedStorage")
  	local RequestCommand = ReplicatedStorage:WaitForChild("HDAdminHDClient").Signals.RequestCommandSilent
  
  	RequestCommand:InvokeServer(";time 12")
  
  
  local ReplicatedStorage = game:GetService("ReplicatedStorage")
  	local RequestCommand = ReplicatedStorage:WaitForChild("HDAdminHDClient").Signals.RequestCommandSilent
  
  	RequestCommand:InvokeServer(";time 0")
  
  local ReplicatedStorage = game:GetService("ReplicatedStorage")
  	local RequestCommand = ReplicatedStorage:WaitForChild("HDAdminHDClient").Signals.RequestCommandSilent
  
  	RequestCommand:InvokeServer(";time 0")
  
  local ReplicatedStorage = game:GetService("ReplicatedStorage")
  	local RequestCommand = ReplicatedStorage:WaitForChild("HDAdminHDClient").Signals.RequestCommandSilent
  
  	RequestCommand:InvokeServer(";time 12")
  
  
  local ReplicatedStorage = game:GetService("ReplicatedStorage")
  	local RequestCommand = ReplicatedStorage:WaitForChild("HDAdminHDClient").Signals.RequestCommandSilent
  
  	RequestCommand:InvokeServer(";time 0")
  
  local ReplicatedStorage = game:GetService("ReplicatedStorage")
  	local RequestCommand = ReplicatedStorage:WaitForChild("HDAdminHDClient").Signals.RequestCommandSilent
  
  	RequestCommand:InvokeServer(";time 0")
  
  local ReplicatedStorage = game:GetService("ReplicatedStorage")
  	local RequestCommand = ReplicatedStorage:WaitForChild("HDAdminHDClient").Signals.RequestCommandSilent
  
  	RequestCommand:InvokeServer(";time 12")
  
  
  local ReplicatedStorage = game:GetService("ReplicatedStorage")
  	local RequestCommand = ReplicatedStorage:WaitForChild("HDAdminHDClient").Signals.RequestCommandSilent
  
  	RequestCommand:InvokeServer(";time 0")
  
  local ReplicatedStorage = game:GetService("ReplicatedStorage")
  	local RequestCommand = ReplicatedStorage:WaitForChild("HDAdminHDClient").Signals.RequestCommandSilent
  
  	RequestCommand:InvokeServer(";time 0")
  
  local ReplicatedStorage = game:GetService("ReplicatedStorage")
  	local RequestCommand = ReplicatedStorage:WaitForChild("HDAdminHDClient").Signals.RequestCommandSilent
  
  	RequestCommand:InvokeServer(";time 12")
  
  
  local ReplicatedStorage = game:GetService("ReplicatedStorage")
  	local RequestCommand = ReplicatedStorage:WaitForChild("HDAdminHDClient").Signals.RequestCommandSilent
  
  	RequestCommand:InvokeServer(";time 0")
  
  local ReplicatedStorage = game:GetService("ReplicatedStorage")
  	local RequestCommand = ReplicatedStorage:WaitForChild("HDAdminHDClient").Signals.RequestCommandSilent
  
  	RequestCommand:InvokeServer(";time 0")
  
  local ReplicatedStorage = game:GetService("ReplicatedStorage")
  	local RequestCommand = ReplicatedStorage:WaitForChild("HDAdminHDClient").Signals.RequestCommandSilent
  
  	RequestCommand:InvokeServer(";time 12")
  
  
  local ReplicatedStorage = game:GetService("ReplicatedStorage")
  	local RequestCommand = ReplicatedStorage:WaitForChild("HDAdminHDClient").Signals.RequestCommandSilent
  
  	RequestCommand:InvokeServer(";time 0")
  
  local ReplicatedStorage = game:GetService("ReplicatedStorage")
  	local RequestCommand = ReplicatedStorage:WaitForChild("HDAdminHDClient").Signals.RequestCommandSilent
  
  	RequestCommand:InvokeServer(";time 0")
  
  local ReplicatedStorage = game:GetService("ReplicatedStorage")
  	local RequestCommand = ReplicatedStorage:WaitForChild("HDAdminHDClient").Signals.RequestCommandSilent
  
  	RequestCommand:InvokeServer(";time 12")
  
  
  local ReplicatedStorage = game:GetService("ReplicatedStorage")
  	local RequestCommand = ReplicatedStorage:WaitForChild("HDAdminHDClient").Signals.RequestCommandSilent
  
  	RequestCommand:InvokeServer(";time 0")
  
  local ReplicatedStorage = game:GetService("ReplicatedStorage")
  	local RequestCommand = ReplicatedStorage:WaitForChild("HDAdminHDClient").Signals.RequestCommandSilent
  
  	RequestCommand:InvokeServer(";time 0")
  
  local ReplicatedStorage = game:GetService("ReplicatedStorage")
  	local RequestCommand = ReplicatedStorage:WaitForChild("HDAdminHDClient").Signals.RequestCommandSilent
  
  	RequestCommand:InvokeServer(";time 12")
  
  
  local ReplicatedStorage = game:GetService("ReplicatedStorage")
  	local RequestCommand = ReplicatedStorage:WaitForChild("HDAdminHDClient").Signals.RequestCommandSilent
  
  	RequestCommand:InvokeServer(";time 0")
  
  local ReplicatedStorage = game:GetService("ReplicatedStorage")
  	local RequestCommand = ReplicatedStorage:WaitForChild("HDAdminHDClient").Signals.RequestCommandSilent
  
  	RequestCommand:InvokeServer(";time 0")
  
  local ReplicatedStorage = game:GetService("ReplicatedStorage")
  	local RequestCommand = ReplicatedStorage:WaitForChild("HDAdminHDClient").Signals.RequestCommandSilent
  
  	RequestCommand:InvokeServer(";time 12")
  
  
  local ReplicatedStorage = game:GetService("ReplicatedStorage")
  	local RequestCommand = ReplicatedStorage:WaitForChild("HDAdminHDClient").Signals.RequestCommandSilent
  
  	RequestCommand:InvokeServer(";time 0")
  
  local ReplicatedStorage = game:GetService("ReplicatedStorage")
  	local RequestCommand = ReplicatedStorage:WaitForChild("HDAdminHDClient").Signals.RequestCommandSilent
  
  	RequestCommand:InvokeServer(";time 0")
  
  local ReplicatedStorage = game:GetService("ReplicatedStorage")
  	local RequestCommand = ReplicatedStorage:WaitForChild("HDAdminHDClient").Signals.RequestCommandSilent
  
  	RequestCommand:InvokeServer(";time 12")
  
  
  local ReplicatedStorage = game:GetService("ReplicatedStorage")
  	local RequestCommand = ReplicatedStorage:WaitForChild("HDAdminHDClient").Signals.RequestCommandSilent
  
  	RequestCommand:InvokeServer(";time 0")
  
  local ReplicatedStorage = game:GetService("ReplicatedStorage")
  	local RequestCommand = ReplicatedStorage:WaitForChild("HDAdminHDClient").Signals.RequestCommandSilent
  
  	RequestCommand:InvokeServer(";time 0")
  
  local ReplicatedStorage = game:GetService("ReplicatedStorage")
  	local RequestCommand = ReplicatedStorage:WaitForChild("HDAdminHDClient").Signals.RequestCommandSilent
  
  	RequestCommand:InvokeServer(";time 12")
  
  
  local ReplicatedStorage = game:GetService("ReplicatedStorage")
  	local RequestCommand = ReplicatedStorage:WaitForChild("HDAdminHDClient").Signals.RequestCommandSilent
  
  	RequestCommand:InvokeServer(";time 0")
  
  local ReplicatedStorage = game:GetService("ReplicatedStorage")
  	local RequestCommand = ReplicatedStorage:WaitForChild("HDAdminHDClient").Signals.RequestCommandSilent
  
  	RequestCommand:InvokeServer(";time 0")
  
  local ReplicatedStorage = game:GetService("ReplicatedStorage")
  	local RequestCommand = ReplicatedStorage:WaitForChild("HDAdminHDClient").Signals.RequestCommandSilent
  
  	RequestCommand:InvokeServer(";time 12")
  
  
  local ReplicatedStorage = game:GetService("ReplicatedStorage")
  	local RequestCommand = ReplicatedStorage:WaitForChild("HDAdminHDClient").Signals.RequestCommandSilent
  
  	RequestCommand:InvokeServer(";time 0")
      
  `,
    "particles": `
  local player = game.Players.LocalPlayer
  
  local char = player.Character
  
  local tool
  
  for i,v in player:GetDescendants() do
  
  	if v.Name == "SyncAPI" then		tool = v.Parent
  
  	end
  
  end
  
  for i,v in game.ReplicatedStorage:GetDescendants() do
  
  	if v.Name == "SyncAPI" then
  
  		tool = v.Parent
  
  	end
  
  end
  
  local remote = tool.SyncAPI.ServerEndpoint
  
  function _(args)
  
  	remote:InvokeServer(unpack(args))
  
  end
  
  function SetCollision(part,boolean)
  
  	local args = {
  
  		[1] = "SyncCollision",
  
  		[2] = {
  
  			[1] = {
  
  				["Part"] = part,
  
  				["CanCollide"] = boolean
  
  			}
  
  		}
  
  	}
  
  	_(args)
  
  end
  
  function SetAnchor(boolean,part)
  
  	local args = {
  
  		[1] = "SyncAnchor",
  
  		[2] = {
  
  			[1] = {
  
  				["Part"] = part,
  
  				["Anchored"] = boolean
  
  			}
  
  		}
  
  	}
  
  	_(args)
  
  end
  
  function CreatePart(cf,parent)
  
  	local args = {
  
  		[1] = "CreatePart",
  
  		[2] = "Normal",
  
  		[3] = cf,
  
  		[4] = parent
  
  	}
  
  	_(args)
  
  end
  
  function DestroyPart(part)
  
  	local args = {
  
  		[1] = "Remove",
  
  		[2] = {
  
  			[1] = part
  
  		}
  
  	}
  
  	_(args)
  
  end
  
  function MovePart(part,cf)
  
  	local args = {
  
  		[1] = "SyncMove",
  
  		[2] = {
  
  			[1] = {
  
  				["Part"] = part,
  
  				["CFrame"] = cf
  
  			}
  
  		}
  
  	}
  
  	_(args)
  
  end
  
  function Resize(part,size,cf)
  
  	local args = {
  
  		[1] = "SyncResize",
  
  		[2] = {
  
  			[1] = {
  
  				["Part"] = part,
  
  				["CFrame"] = cf,
  
  				["Size"] = size
  
  			}
  
  		}
  
  	}
  
  	_(args)
  
  end
  
  function AddMesh(part)
  
  	local args = {
  
  		[1] = "CreateMeshes",
  
  		[2] = {
  
  			[1] = {
  
  				["Part"] = part
  
  			}
  
  		}
  
  	}
  
  	_(args)
  
  end
  
  function SetMesh(part,meshid)
  
  	local args = {
  
  		[1] = "SyncMesh",
  
  		[2] = {
  
  			[1] = {
  
  				["Part"] = part,
  
  				["MeshId"] = "rbxassetid://"..meshid
  
  			}
  
  		}
  
  	}
  
  	_(args)
  
  end
  
  function SetTexture(part, texid)
  
  	local args = {
  
  		[1] = "SyncMesh",
  
  		[2] = {
  
  			[1] = {
  
  				["Part"] = part,
  
  				["TextureId"] = "rbxassetid://"..texid
  
  			}
  
  		}
  
  	}
  
  	_(args)
  
  end
  
  function SetName(part, stringg)
  
  	local args = {
  
  		[1] = "SetName",
  
  		[2] = {
  
  			[1] = part
  
  		},
  
  		[3] = stringg
  
  	}
  
  	_(args)
  
  end
  
  function MeshResize(part,size)
  
  	local args = {
  
  		[1] = "SyncMesh",
  
  		[2] = {
  
  			[1] = {
  
  				["Part"] = part,
  
  				["Scale"] = size
  
  			}
  
  		}
  
  	}
  
  	_(args)
  
  end
  
  function Weld(part1, part2,lead)
  
  	local args = {
  
  		[1] = "CreateWelds",
  
  		[2] = {
  
  			[1] = part1,
  
  			[2] = part2
  
  		},
  
  		[3] = lead
  
  	}
  
  	_(args)
  
  end
  
  function SetLocked(part,boolean)
  
  	local args = {
  
  		[1] = "SetLocked",
  
  		[2] = {
  
  			[1] = part
  
  		},
  
  		[3] = boolean
  
  	}
  
  	_(args)
  
  end
  
  function SetTrans(part,int)
  
  	local args = {
  
  		[1] = "SyncMaterial",
  
  		[2] = {
  
  			[1] = {
  
  				["Part"] = part,
  
  				["Transparency"] = int
  
  			}
  
  		}
  
  	}
  
  	_(args)
  
  end
  
  function CreateSpotlight(part)
  
  	local args = {
  
  		[1] = "CreateLights",
  
  		[2] = {
  
  			[1] = {
  
  				["Part"] = part,
  
  				["LightType"] = "SpotLight"
  
  			}
  
  		}
  
  	}
  
  	_(args)
  
  end
  
  function SyncLighting(part,brightness)
  
  	local args = {
  
  		[1] = "SyncLighting",
  
  		[2] = {
  
  			[1] = {
  
  				["Part"] = part,
  
  				["LightType"] = "SpotLight",
  
  				["Brightness"] = brightness
  
  			}
  
  		}
  
  	}
  
  	_(args)
  
  end
  
  function Color(part,color)
  
  	local args = {
  
  		[1] = "SyncColor",
  
  		[2] = {
  
  			[1] = {
  
  				["Part"] = part,
  
  				["Color"] = color,
  
  				["UnionColoring"] = false
  
  			}
  
  		}
  
  	}
  
  	_(args)
  
  end
  
  function SpawnDecal(part,side)
  
  	local args = {
  
  		[1] = "CreateTextures",
  
  		[2] = {
  
  			[1] = {
  
  				["Part"] = part,
  
  				["Face"] = side,
  
  				["TextureType"] = "Decal"
  
  			}
  
  		}
  
  	}
  
  	_(args)
  
  end
  
  function AddDecal(part,asset,side)
  
  	local args = {
  
  		[1] = "SyncTexture",
  
  		[2] = {
  
  			[1] = {
  
  				["Part"] = part,
  
  				["Face"] = side,
  
  				["TextureType"] = "Decal",
  
  				["Texture"] = "rbxassetid://".. asset
  
  			}
  
  		}
  
  	}
  
  	_(args)
  
  end
  
  -- Ã°Å¸âÂ¹ Tambahan: daftar 3 ID decal
  
  local ids = {
  
  	"82289120460383", -- ID 1
  
  	"94578277744548", -- ID 2
  
  	"105730768454228"  -- ID 3
  
  }
  
  while wait(0.1) do
  
  	spawn(function()
  
  		local e = char.HumanoidRootPart.CFrame.x + math.random(-100, 100)
  
  		local f = char.HumanoidRootPart.CFrame.y
  
  		local g = char.HumanoidRootPart.CFrame.z + math.random(-100, 100)
  
  		CreatePart(CFrame.new(math.floor(e), math.floor(f), math.floor(g)) + Vector3.new(0,6,0), workspace)
  
  		for i,v in game.Workspace:GetDescendants() do
  
  			if v:IsA("BasePart") and v.CFrame.x == math.floor(e) and v.CFrame.z == math.floor(g) then
  
  				SetName(v,"particle by expl_0itspooky")
  
  				-- Ã°Å¸âÂ¹ pilih salah satu ID acak dari daftar di atas
  
  				local id = ids[math.random(1, #ids)]
  
  				SpawnDecal(v,Enum.NormalId.Front)
  
  				AddDecal(v,id,Enum.NormalId.Front)
  
  				SpawnDecal(v,Enum.NormalId.Back)
  
  				AddDecal(v,id,Enum.NormalId.Back)
  
  				SetTrans(v,1)
  
  				Resize(v,Vector3.new(7,7,0.1),v.CFrame)
  
  				SetLocked(v,true)
  
  				while wait(0.01) do
  
  					MovePart(v,CFrame.new(v.CFrame.x,v.CFrame.y + 1,v.CFrame.z))
  
  				end
  
  			end
  
  		end
  
  	end)
  
  end 
  `
  };
  
  // Mostrar script no textarea
  function run() {
    let cmd = document.getElementById('cmd').value.toLowerCase().replace('/', '');
    const out = document.getElementById('out');
    if(commands[cmd]) {
      out.value = commands[cmd];
    } else out.value = 'Command not found';
  }
  
  // Copiar para clipboard
  function copyScript() {
    const out = document.getElementById('out');
    out.select();
    navigator.clipboard.writeText(out.value);
    alert("Copied!");
  }
  
  // Baixar como .txt
  function downloadScript() {
    let filename = prompt("Enter file name:", "script");
    if(!filename) return;
    const blob = new Blob([document.getElementById('out').value], {type: "text/plain"});
    const link = document.createElement("a");
    link.download = filename + ".txt";
    link.href = URL.createObjectURL(blob);
    link.click();
  }
  
  // Filtrar lista de comandos
  function filterCommands() {
    let filter = document.getElementById('search').value.toLowerCase();
    const list = document.getElementById('command-list');
    const items = list.getElementsByTagName('p');
    for(let i=0;i<items.length;i++){
      let txt = items[i].textContent || items[i].innerText;
      items[i].style.display = txt.toLowerCase().includes(filter) ? "" : "none";
    }
  }
 </script>

 <div id="footer">Made for F3X scripts</div>
</body>

</html>