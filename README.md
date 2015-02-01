# joystick
joystick for cocos2d-x v3.3

# 核心思想
* 解耦，采用事件机制将joystick的事件和目标的关联进行解耦

# 实现思路
* 1.继承自layer并注册监听touch event
* 2.若touch事件在joystick的中心点触发的，则继续下面的逻辑
* 3.更新joystick中心点的位置
* 4.计算touch点joystick中心点的角度(角度范围，第一象限[0, 90], 第二象限[90, 180]， 第三象限[-180, -90]， 第四象限[-90, 0])
* 5.发布自定义的joystick event，目前事件仅包含上面计算的角度值，可根据需要进行增改
* 6.注册joystick event的事件监听器，并在回调函数里实现你的业务逻辑
* 7.joystick event中的userdata的内存释放，交给auto-release-pool了， 具体见JoystickEvent的实现

# 核心代码
* 见joystick的touch事件的处理部分

# 集成到项目
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

# 参考资料
* https://github.com/cheyiliu/All-in-One/wiki/cocos2d-x-3.3-012-%E4%BA%8B%E4%BB%B6%E5%88%86%E5%8F%91%E6%9C%BA%E5%88%B6
* http://blog.csdn.net/evankaka/article/details/42043509

