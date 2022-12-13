### @explicitHints 1

```template
let 번호 = 0
player.onChat("시작", function () {
    gameplay.title(mobs.target(NEAREST_PLAYER), "게임시작!", "양털블록을 부셔 문제를 보고 좀비를 죽여 번호를 선택하세요")
    player.say("게임 방법1. 양털블록을 부시면 문제가 나옵니다. 몇번 문제인지 기억하세요.")
    player.say("게임 방법2. 정답이 몇번인지 생각한뒤, 좀비를 잡아 정답인 번호를 선택하세요.")
    player.say("게임 밥업3. 번호를 선택했으면, 채팅창에 '0번정답'이라고 외치세요")
    번호 = 0
    번호 = 0
    builder.teleportTo(pos(0, 0, 0))
    builder.move(FORWARD, 2)
    builder.place(WOOL)
    builder.move(FORWARD, 2)
    builder.place(ORANGE_WOOL)
    builder.move(FORWARD, 2)
    builder.place(MAGENTA_WOOL)
    gameplay.setWeather(RAIN)
    gameplay.setDifficulty(EASY)
    gameplay.setGameMode(
    SURVIVAL,
    mobs.target(NEAREST_PLAYER)
    )
    gameplay.timeSet(gameplay.time(NIGHT))
    for (let index = 0; index < 100; index++) {
        mobs.spawn(mobs.monster(ZOMBIE), pos(50, 10, 50))
    }
})

```

# 우주로켓 발사 미션

## 단계 1 
### 소제목
이런 저런 내용을 적습니다.
``||Player:채팅창에 말하기||``의 채팅명령어를 **발사**로 적으세요.

## 단계 2 
``||loops:반복(for)||``를 가져와 **index**의 반복값을 **100**으로 바꾸세요.
``||blocks:블록 복사하기||``를 가져온 뒤 **마스크설정**을 **마스크**로, **복사설정**을 **이동**으로 바꾸세요.

## 단계 3 
``||Positions:좌표더하기||``를 가져와 블록복사하기의 시작, 끝, 목적지 좌표값에 넣으세요. 
``||Positions:월드 좌표||``를 가져와 블록복사하기 시작 좌푯값을 **-288, 65, -6880** 으로 입력하세요.
같은 방법으로 ``||Positions:월드 좌표||``를 두번 가져와 끝 좌푯값에는 **-294, 71, -6885**을 입력하세요.
목적지 좌푯값에는 **-294, 65, -6885**를 입력하세요.

### ~ tutorialhint
``` blocks
player.onChat("발사", function () {
    for (let index = 0; index <= 100; index++) {
        blocks.clone(
        positions.add(
        world(-288, 65, -6880),
        pos(0, 0, 0)
        ),
        positions.add(
        world(-294, 71, -6885),
        pos(0, 0, 0)
        ),
        positions.add(
        world(-294, 65, -6885),
        pos(0, 0, 0)
        ),
        CloneMask.Masked,
        CloneMode.Move
        )
    }
})
```

## 단계 4 
``||Valueable:변수 index||``를 가져온 뒤 블록 복사하기의 시작과 끝의 좌표더하기 값 가운데 **y좌표**에 넣으세요.
단 목적지 좌표값은 index에서 1을 더한 값으로 입력하세요. 목적지 y좌표에 1을 더한 이유는 1칸씩 위로 이동한다는 뜻이에요.
``||loops:일시중지||``를 가져와 블록 복사하기 아래에 넣고 값을 **300**으로 입력하세요. 시간이 짧을수록 더 빨리 이동해요.


### ~ tutorialhint
``` blocks
let 번호 = 0
let 점수 = 0
mobs.onMobKilled(mobs.monster(ZOMBIE), function () {
    번호 += 1
    player.say("당신은" + 번호 + "번을 선택합니다.")
})
player.onChat("종료", function () {
    player.say("당신의 점수는" + 점수 + "점입니다.")
    점수 = 0
})
blocks.onBlockPlaced(ORANGE_WOOL, function () {
    player.say("2번 문제: 이산화탄소를 배출한 만큼 이산화탄소를 흡수하여 이사놔탄소의 배출량을 "0"으로 만든다는 개념은?")
    player.say("1번: 탄소흡수, 2번: 탄소중립, 3번: 탄소배출")
})
player.onChat("1번 정답", function () {
    if (번호 == 1) {
        player.say("오답입니다.")
        mobs.spawn(LIGHTNING_BOLT, pos(0, 0, 0))
    } else if (번호 == 2) {
        player.say("오답입니다.")
        mobs.spawn(LIGHTNING_BOLT, pos(0, 0, 0))
    } else {
        player.say("축하합니다. 정답입니다.")
        mobs.spawn(FIREWORKS_ROCKET, pos(0, 0, 0))
        점수 += 1
    }
})
blocks.onBlockPlaced(MAGENTA_WOOL, function () {
    player.say("3번 문제: 다음 중 탄소중립을 위한 생활 속 실천이아닌 것은 무엇일까요?")
    player.say("1번: 나무심기, 2번: 카페 갈때 텀블러 챙기기, 3번: 밤새 TV 틀고 자기")
})
player.onChat("3번정답", function () {
    if (번호 == 1) {
        player.say("오답입니다.")
        mobs.spawn(LIGHTNING_BOLT, pos(0, 0, 0))
    } else if (번호 == 2) {
        player.say("오답입니다.")
        mobs.spawn(LIGHTNING_BOLT, pos(0, 0, 0))
    } else {
        player.say("축하합니다. 정답입니다.")
        mobs.spawn(FIREWORKS_ROCKET, pos(0, 0, 0))
        점수 += 1
    }
})
player.onChat("2번정답", function () {
    if (번호 == 1) {
        player.say("오답입니다.")
        mobs.spawn(LIGHTNING_BOLT, pos(0, 0, 0))
    } else if (번호 == 2) {
        player.say("축하합니다. 정답입니다.")
        mobs.spawn(FIREWORKS_ROCKET, pos(0, 0, 0))
        점수 += 1
    } else {
        player.say("오답입니다.")
        mobs.spawn(LIGHTNING_BOLT, pos(0, 0, 0))
    }
})
player.onChat("시작", function () {
    gameplay.title(mobs.target(NEAREST_PLAYER), "게임시작!", "양털블록을 부셔 문제를 보고 좀비를 죽여 번호를 선택하세요")
    player.say("게임 방법1. 양털블록을 부시면 문제가 나옵니다. 몇번 문제인지 기억하세요.")
    player.say("게임 방법2. 정답이 몇번인지 생각한뒤, 좀비를 잡아 정답인 번호를 선택하세요.")
    player.say("게임 밥업3. 번호를 선택했으면, 채팅창에 '0번정답'이라고 외치세요")
    번호 = 0
    번호 = 0
    builder.teleportTo(pos(0, 0, 0))
    builder.move(FORWARD, 2)
    builder.place(WOOL)
    builder.move(FORWARD, 2)
    builder.place(ORANGE_WOOL)
    builder.move(FORWARD, 2)
    builder.place(MAGENTA_WOOL)
    gameplay.setWeather(RAIN)
    gameplay.setDifficulty(EASY)
    gameplay.setGameMode(
    SURVIVAL,
    mobs.target(NEAREST_PLAYER)
    )
    gameplay.timeSet(gameplay.time(NIGHT))
    for (let index = 0; index < 100; index++) {
        mobs.spawn(mobs.monster(ZOMBIE), pos(50, 10, 50))
    }
})
player.onChat("번호초기화", function () {
    점수 = 0
    player.say("당신은" + 번호 + "번을 선택합니다.")
})
blocks.onBlockPlaced(WOOL, function () {
    player.say("1번 문제: 대기중 온실가스가 온실의 유리처럼 적용하여 지구표면의 온도를 유지하는 것은 무슨 효과일까요?")
    player.say("1번: 비닐효과, 2번: 온난효과, 3번 : 온실효과")
})


```