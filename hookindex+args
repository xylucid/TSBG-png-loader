local securehook = function(object, method, hook)
    return hookfunction(getrawmetatable(object)[method], hook)
end


local indexMethods = {
    ["VoiceChatInternal"] = true,
    ["VoiceChatService"] = true,
}


oldindex = securehook(game, "__index", function(self, key)
    local og = oldindex(self, key)

    if not checkcaller() then
        return og
    end

    local object = tostring(self)

    if indexMethods[object] and key ~= "IsPublishPaused" then
        if typeof(og) == "function" then
            return function(...)
                local args = {...}
                print(tostring(self), key)
                for i,v in args do
                    print(string.format("Args[%d] {%s} = %s", i, typeof(v), tostring(v)))
                end
                return og(...)
            end   
        end
    end
    return og 
end)
print("Tracking __index")

