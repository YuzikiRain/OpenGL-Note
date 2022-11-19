## 绘制到自定义面板而不是默认窗口

需要使用分支docking

``` c++
ImGui::Begin(name, &isOpen, ImGuiWindowFlags_None);

// 渲染到帧缓冲（附件为纹理）
glBindFramebuffer(GL_FRAMEBUFFER, fbo);
glClearColor(0, 0, .4, 0);
glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT);

ImVec2 wsize = ImGui::GetWindowSize();

// 绘制一些东西

glFramebufferTexture2D(GL_FRAMEBUFFER, GL_COLOR_ATTACHMENT0, GL_TEXTURE_2D, texture, 0);
glBindFramebuffer(GL_FRAMEBUFFER, 0);

// Using a Child allow to fill all the space of the window.
// It also alows customization
ImGui::BeginChild("GameRender");
// Get the size of the child (i.e. the whole draw size of the windows).

// Because I use the texture from OpenGL, I need to invert the V from the UV.
ImGui::Image((ImTextureID)texture, wsize, ImVec2(0, 1), ImVec2(1, 0));
ImGui::EndChild();

ImGui::End();
```

