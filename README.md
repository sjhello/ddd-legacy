# 키친포스

## 퀵 스타트

```sh
cd docker
docker compose -p kitchenpos up -d
```

## 요구 사항

- 상품
    - [ ] 상품을 추가 할 수 있다.
        - [ ] 상품의 가격은 null 이거나 0보다 작을 수 없다.
        - [ ] 상품의 이름이 null 이거나 등록하려는 상품 이름이 https://www.purgomalum.com 에 존재 한다면 상품을 등록 할 수 없다.
    - [ ] 상품의 가격을 변경 할 수 있다.
        - [ ] 상품의 가격은 null 이거나 0보다 작을 수 없다.
        - [ ] 상품의 가격이 변경되면 해당 상품이 등록되어 있는 메뉴의 가격이 메뉴에 등록되어 있는 메뉴 상품의 가격의 합보다 클 경우에는 메뉴를 숨김 처리 한다.
    - [ ] 상품의 목록을 볼 수 있다.
- 메뉴 그룹
    - [ ] 메뉴 그룹을 추가 할 수 있다.
        - [ ] 메뉴 그룹의 이름은 null이거나 공백 일 수 없다.
    - [ ] 메뉴 그룹 목록을 볼 수 있다.
- 메뉴
    - [ ] 메뉴를 추가 하려면 메뉴 그룹, 상품을 먼저 등록 해야 한다.
        - [ ] 메뉴는 하나 이상의 메뉴 그룹에 속해 있어야 한다.
        - [ ] 메뉴에 등록되는 상품을 메뉴 상품이라고 하며 메뉴 상품은 하나 이상 등록되어야 한다.
            - [ ] 메뉴 상품은 상품 id와 수량으로 이루어져 있다.
        - [ ] 메뉴의 가격은 메뉴 상품 가격의 총 합보다 클 수 없다.
        - [ ] 메뉴의 이름은 null이 거나 등록하려는 메뉴 이름이 https://www.purgomalum.com 에 존재 한다면 메뉴를 등록 할 수 없다.
    - [ ] 메뉴의 가격을 변경 할 수 있다.
        - [ ] 가격은 0보다 작을 수 없고 null이 될 수 없다.
        - [ ] 수정하려는 메뉴의 가격은 메뉴 상품 가격의 총 합보다 클 수 없다.
    - [ ] 메뉴를 사용자들에게 보이게 할 수도 있고, 보이지 않게 할 수도 있다.
        - [ ] 메뉴를 사용자들에게 보이게 하는 것을 "메뉴 전시"라고 한다.
            - [ ] 메뉴의 가격이 메뉴 상품 가격의 총 합보다 작을 때에만 메뉴를 전시 할 수 있다.
        - [ ] 메뉴를 사용자들에게 보이지 않게 하는 것을 "메뉴 숨김" 이라고 한다.
    - [ ] 메뉴의 목록을 볼 수 있다.
- 주문 테이블
    - [ ] 지정한 이름으로 주문 테이블을 생성 할 수 있다.
    - [ ] 주문 테이블에 손님이 식사를 할 수 있다.
    - [ ] 주문의 상태가 완료가 아닌 경우에는 해당 주문 테이블을 비울 수 없다.
    - [ ] 주문 테이블에 손님의 수를 바꿀 수 있는 경우는 해당 주문 테이블에 손님이 있어야 한다.
    - [ ] 주문 테이블의 목록을 볼 수 있다.
- 주문
    - [ ] 주문은 대기, 수락, 제공됨, 배달중, 배달완료, 완료 라는 상태를 갖는다.
    - [ ] 주문은 배달, 포장, 매장 식사 라는 타입을 갖는다.
    - [ ] 매장 식사 주문인 경우에
        - [ ] 주문을 한 손님이 어느 테이블에 있는지 알 수 있다.
        - [ ] 주문의 상태는 대기 -> 수락 -> 제공됨 -> 완료 의 순서를 갖는다.
        - [ ] 매장 손님이 식사를 완료하면 손님이 앉았던 테이블의 상태는 미점거 상태가 된다.
    - [ ] 포장 주문인 경우에
        - [ ] 주문의 상태는 대기 -> 수락 -> 제공됨 -> 완료 의 순서를 갖는다.
    - [ ] 배달 주문인 경우에
        - [ ] 주문의 상태는 대기 -> 수락 -> 제공됨 -> 배달시작 -> 배달완료 -> 완료 의 순서를 갖는다.
        - [ ] 배달 주소가 없으면 주문 할 수 없다.
        - [ ] 주문(배달)을 수락하면 키친 라이더에게 주문 id, 주문한 메뉴의 합계, 배달 주소를 전달한다.
    - [ ] 주문을 하려면 주문의 타입, 주문서가 필요하다
        - [ ] 주문서는 메뉴, 메뉴의 가격, 수량이 있어야 한다.
        - [ ] 등록되어 있지 않은 메뉴는 주문 할 수 없다.
        - [ ] 메뉴의 수량은 0보다 작을 수 없다.
        - [ ] 주문 하려하는 메뉴가 전시되어 있어야 한다.
        - [ ] 음식 주문서에 있는 메뉴의 가격과 등록되어진 메뉴의 가격은 동일해야 한다.
        - [ ] 주문이 성공적으로 되면 주문의 상태는 대기가 된다.

## 용어 사전

| 한글명   | 영문명         | 설명                  |
|-------|-------------|---------------------|
| 메뉴 상품 | MenuProduct | 메뉴에 등록되어 있는 상품      |
| 전시    | display     | 메뉴를 사용자에게 보여준다.     |
| 숨김    | hide        | 메뉴를 사용자에게 보여주지 않는다. |

## 모델링
