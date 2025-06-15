function love.load()
    button = {x = 100, y = 100, width = 200, height = 50}
    buttonText = "Tıkla!"
    message = ""
end

function love.draw()
    -- Butonu çiz
    love.graphics.setColor(0.3, 0.6, 1)
    love.graphics.rectangle("fill", button.x, button.y, button.width, button.height)
    love.graphics.setColor(1, 1, 1)
    love.graphics.printf(buttonText, button.x, button.y + 15, button.width, "center")
    
    -- Mesajı çiz
    love.graphics.setColor(1, 1, 1)
    love.graphics.print(message, 100, 200)
end

function love.mousepressed(x, y, buttonType, isTouch)
    if buttonType == 1 then -- Sol tık
        if x > button.x and x < button.x + button.width and
           y > button.y and y < button.y + button.height then
            message = "Butona tıkladın!"
        end
    end
end
