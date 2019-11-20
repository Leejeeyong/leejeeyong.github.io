---
title:  "[Unity]Deag&Drop"
search: false
categories: 
  - markdown
last_modified_at: 2019-11-20T08:06:00-05:00
---

```

```

![img](http://cfile21.uf.tistory.com/image/994A8B335A2A37290945C3)





먼저 Canvas를 하나 만들어줍니다.

이름은 MainUI로 합니다.



그리고 MainUI에 드래그할 오브젝트 추가를 위해서

UI>Image를 추가해줍니다.

이름은 Drag1로 합니다.



![img](http://cfile26.uf.tistory.com/image/994B23335A2A37282002E5)



소스이미지를 원하는 것으로 바꿉니다.

저는 Knob로 설정했습니다.



그리고 3개를 더 만들어주고 구분하기 위해서 Color를 서로 다른 색으로 바꿉니다.

각각 Drag1, Drag2, Drag3, Drag4로 이름을 바꿔줍니다.



![img](http://cfile30.uf.tistory.com/image/99C6F3335A2A372805EF76)



스크립트는 CircleDragScript를 만듧니다.

사진에 MainScript는 드롭을 할때부터 이용되는 것이라

지금은 안 만드셔도 상관은 없습니다.



![img](http://cfile10.uf.tistory.com/image/9920F4335A2A37292EDDB9)



CirecleDragScript를 드래그해서 Drag1~4에 각각 드래그앤드롭해줍니다.



이제 스크립트를 작성하기위해서 CirecleDragScript를 더블클릭해서 IDE를 켜줍니다.



![img](http://cfile26.uf.tistory.com/image/99CAEE335A2A3728340B18)



가장먼저 상단에 인터페이스를 추가합니다.

MonoBehaviour옆에 

IBeginDragHandler, IEndDragHandler, IDragHandler 

이것들을 추가해줍니다.



그리고 드래그하고 드롭하면 다시 원위치로 돌려보내기 위한 변수로

public static Vector2 defaultposition; 이것을 추가해줍니다.





```c#
public class CircleDragScript : MonoBehaviour, IBeginDragHandler, IEndDragHandler, IDragHandler
{
     public static Vector2 defaultposition;//드롭하면 다시 원위치로 보내기위한 변수

     void Start () {
         }
     void Update () {
          }
}
```

![img](http://cfile10.uf.tistory.com/image/99A339335A2A372821BCCB)



빨간줄이 그어지면 마우스를 위에 올리시고 잠재적수정사항을 누릅니다.

![img](http://cfile30.uf.tistory.com/image/99430B335A2A372931785A)

그리고 인터페이스추가를 누르면

![img](http://cfile21.uf.tistory.com/image/99AD67335A2A372937B11F)



인터페이스가 추가됩니다.

3개를 모두 해주고

보기좋게 하기 위해서 

Update아래로 옮겨줍니다.

![img](http://cfile6.uf.tistory.com/image/99AE55335A2A3729238840)



```c#
void IBeginDragHandler.OnBeginDrag(PointerEventData eventData)//드래그시작할 때
    {
       defaultposition = this.transform.position;
      }
```

가장 먼저 드래그를 시작할때 처음위치로 다시 돌려보내기위해서

처음위치의 좌표를 저장해줍니다.

```
void IDragHandler.OnDrag(PointerEventData eventData)//드래그중일 때
     {
        Vector2 currentPos = Input.mousePosition;
        this.transform.position = currentPos;
      }
```

그리고 드래그중일때는 현재위치를 마우스나 터치지점을 따라가기위해서

마우스포지션을 가져오고 따라가게 오브젝트가 하기위해서

transform.position으로 위치를 지정해줍니다.



```c#
 void IEndDragHandler.OnEndDrag(PointerEventData eventData)//드래그 끝났을 때
    {
      Vector2 mousePos = Camera.main.ScreenToWorldPoint(Input.mousePosition);

       this.transform.position = defaultposition;
     }
```

마지막으로 드래그가 끝났을때 다시 원위치로 돌려보내기 위해서

드래그를 시작할때 원위치의 좌표로 이동시켜 줍니다.



드래그하고 드롭한 위치에 두려면 드롭했을때 마우스의 위치로 이동시켜주면 됩니다.





저장을 하고 유니티로 돌아와서 실행을 해봅니다.



![img](http://cfile28.uf.tistory.com/image/99E31E335A2A372935C15F)



4개의 오브젝트가 제대로 움직이고 드롭하면 원위치로 잘 돌아가는 것을 볼수있습니다.

```alias

```