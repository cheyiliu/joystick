# joystick
joystick for cocos2d-x v3.3

# 详细分析
* https://github.com/cheyiliu/All-in-One/wiki/cocos2d-x-3.3-018-joystick4cocos3.3

# 用法
* 我以proj.linx为例
* 在CMakeLists.txt中增加cpp
```
set(GAME_SRC
  Classes/AppDelegate.cpp
  Classes/HelloWorldScene.cpp
  Classes/Joystick.cpp        #新增
  ${PLATFORM_SPECIFIC_SRC}
)

```
* 注册监听joystick event
```
#include "Joystick.h"


    auto _listener = EventListenerCustom::create(JoystickEvent::EVENT_JOYSTICK, [=](EventCustom* event){
        JoystickEvent* jsevent = static_cast<JoystickEvent*>(event->getUserData());
        log("--------------got joystick event, %p,  angle=%f", jsevent, jsevent->mAnagle);

        // do you business you'd like to
    });

    _eventDispatcher->addEventListenerWithFixedPriority(_listener, 1);
```
