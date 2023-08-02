var Main=(function(){
var root={};
var ui;
root.actorInited = true;
root.ADgameCnt = 0 ;
root.ADgameCnt1 = 0;


root.setUserInfo=function (target){
    var winCount=target.getChildByName("winCount");
    var level=target.getChildByName("level");
    var exp=target.getChildByName("exp");
    var expMax=target.getChildByName("expMax");

    winCount.value=User.winCount;
    level.value=User.level;
    exp.value=User.exp;
    expMax.value=User.getExpMax();
}



root.initUserInfo=function (target){
    var msk=new Laya.Sprite();
    msk.graphics.drawCircle(40,40,40,"#ffffff");
}

function update(){
    DragList.update();
    // if(Math.random()>0.8){
    //     var img=new Laya.Image("ui/f_gb.png");
    //     img.anchorX=0.5;
    //     img.anchorY=0.5;
    //     img.x=Math.random()*Laya.stage.width;
    //     img.y=Math.random()*300;

    //     ui.bg.addChild(img);
    //     img.scale(0.5,0.5);
    //     img.alpha=0;
    //     Laya.Tween.to(img,{scaleX:1,scaleY:1,alpha:1},2000,null,Laya.Handler.create(null,function (){
    //         Laya.Tween.to(img,{scaleX:0.5,scaleY:0.5,alpha:0},2000,null,Laya.Handler.create(null,function (){
    //             img.destroy();
    //         }
    //         ));
    //     }
    //     ))
    // }
}

root.showMsk = function(val){
    if(val){
        var bg=new Laya.Sprite();
        bg.graphics.drawRect(0,0,Laya.stage.width,Laya.stage.height,"#000000");
        bg.alpha=0.8;
        ui.blackbg.addChild(bg);
    }
    else{
        ui.blackbg.removeSelf();
    }
    
}




root.show=function(){
    platform.showBannerAd(1,'c056df467ce7ce9bdeac4a5742ff7136');
    this.AdCompleted1 = false;
    this.AdCompleted2 = false;
    this.AdCompleted3 = false;
    this.CloseShow = false;


    EventMgr.getInstance().on(EEvent.ShowAdCompleted,this,this.ShowAdCompleted);
    EventMgr.getInstance().on(EEvent.CloseShowAd,this,this.CloseShowAd);
    ui.visible=true;
    ui.getskin.visible = false;
    
    
    root.setUserInfo(ui.playerLevel);
    Laya.timer.frameLoop(1,null,update);

    g.tweenFrom(ui.logo,{scaleX:2,scaleY:2},200);
    DragList.show();
    // root.lightBumper.start();
    root.c1Mover.start();
    root.c2Mover.start();
    root.ad5shaker.start();
    if(Result.lvlup){
        var img=new Laya.FontClip("ui/sz.png");
        img.sheet="0123456789";
        img.value=Result.ui.exp.value;
        img.align="center";
        img.x=360;
        img.y=Laya.stage.height/2;
        ui.addChild(img);
        img.scale(1.5,1.5);
        g.once(500,function (){
            g.tweenTo(img,{x:ui.playerLevel.x+100,y:ui.playerLevel.y,scaleX:1,scaleY:1},1200,null,function (){
            img.destroy();
        }
        )
        }
        )
        
    }
}
root.hide=function(){
    EventMgr.getInstance().off(EEvent.ShowAdCompleted,this,this.ShowAdCompleted);
    EventMgr.getInstance().off(EEvent.CloseShowAd,this,this.CloseShowAd);
    ui.visible=false;
    Laya.timer.clear(null,update);
    // root.lightBumper.stop();
    root.c1Mover.stop();
    root.c2Mover.stop();
    root.ad5shaker.stop();
}

root.setSignRedDot=function (){

}

root.ShowAdCompleted = function(pos){
    if(pos==1){
        this.AdCompleted1 = true;
    }
    if(pos==2){
        this.AdCompleted2 = true;
    }
    if(pos==3){
        this.AdCompleted3 = true;
    }
    
}

root.CloseShowAd = function(){
    if(this.AdCompleted1){
        this.AdCompleted1 = false;
        Actor.ad5=true; 
        Match.show();

    }
    if(this.AdCompleted2){ 
        this.AdCompleted2 = false;   
        Match.show();
    }
    if(this.AdCompleted3){ 
        this.AdCompleted3 = false;   
        if(User.WatchSkinAd[18].Cnt<2){
            User.WatchSkinAd[18].Cnt ++;
        }
        
        if(User.WatchSkinAd[18].Cnt>=2){
            User.actors[18].own=true;
        }
        ui.showAdCnt.text = User.WatchSkinAd[18].Cnt;
        User.actor=18;
    }

}

root.init=function(){
    ui=new mainUI();
    root.ui=ui;
    Cord.adjustUI(ui);
    if(Laya.stage.height>1320){
        var s=Laya.stage.height/1320;
        ui.bg.scale(1,s);
    }
    // root.lightBumper=g.createBumper(ui.light,0.8,0.002);
    root.c1Mover=g.createMover(ui.c1,{
        speedX:0.08,
        maxX:-150,
        minX:-384
    });
    root.c2Mover=g.createMover(ui.c2,{
        speedX:0.12,
        maxX:600,
        minX:393
    });

    // LoginID = platform.getLoginID();
    // if(!User.actors[17].own && LoginID == 1001){
    //     User.actors[17].own=true;
    // }
    root.ad5shaker=g.createShaker(ui.ad5);
    ui.ad5.on('click',null,function(){
        platform.showVideoAd(1,'6f821985c9cfedabb12e6572d2a7460f');
        Laya.SoundManager.playSound("sound/btn.mp3");
        // platform.playVideo(function (){
        //     Actor.ad5=true; 
        //     platform.logEvent("ad5Clicked");
        //     Match.show();
        // });
    })

    ui.skinbtn.on('click',null,function(){
        Laya.SoundManager.playSound("sound/btn.mp3");
        if(GameConst.IsClickSkinNeZa){
            var needAdCnt = GameConst.ClickSkinNeZa;
            root.ADgameCnt1 ++;
            if(root.ADgameCnt1 >= needAdCnt){
                Laya.timer.once(GameConst.IsEndAdtime,null,function(){
                    platform.showVideoAd(3,'9ba9885e0723c0924a31d1d5cf22b0ef');
                })
                root.ADgameCnt1 = 0;
            }
        }
        ui.getskin.visible = true;
        ui.showAdCnt.text = User.WatchSkinAd[18].Cnt;
        ui.getskinbg.graphics.drawRect(0,0,Laya.stage.width,Laya.stage.height,"#000000");
        ui.getskinbg.alpha=0.8;
        ui.closeSkinBtn.on('click',null,function(){
            Laya.SoundManager.playSound("sound/btn.mp3");
            ui.getskin.visible = false;
            platform.showinterstitialAd();
        })
        ui.watchADSkin.on('click',null,function(){
            platform.showVideoAd(3,'515aa9462f5fd9cc938a948cf46789b2');
            
            Laya.SoundManager.playSound("sound/btn.mp3");
        })

    });



    root.initUserInfo(ui.playerLevel);
    root.playTimes=0;
    Laya.stage.addChild(ui);
    ui.visible=false;
    ui.btnPlay.on('click',null,function(){
        Laya.SoundManager.playSound("sound/btn.mp3");
        platform.logEvent("playClicked");
        Match.show();
    })
    ui.play2.on('click',null,function(){
        Laya.SoundManager.playSound("sound/btn.mp3");
        platform.share(function (){
            platform.logEvent("play2Clicked");
            Match.show();
        })
    })

    ui.btnCondi.on('click',null,function(){
        platform.showVideoAd(2,'63f8ac1c00c668411f86c5938c794f85');
        // platform.playVideo(function (){
        //      Match.show();

        //     platform.logEvent("aDplayClicked");
        // })

        Laya.SoundManager.playSound("sound/btn.mp3");
        // root.hide();

    })
    ui.btnSign.on('click',null,function(){
        platform.logEvent("signClick");
        Laya.SoundManager.playSound("sound/btn.mp3");
        root.hide();
        Sign.show();
    });
    ui.dragArea.on(Laya.Event.MOUSE_DOWN,null,DragList.onMouseDown);
    ui.on(Laya.Event.MOUSE_MOVE,null,DragList.onMouseMove);
    ui.on(Laya.Event.MOUSE_UP,null,DragList.onMouseUp);
    DragList.init(ui.actor);

    ui.btnskin.on('click',null,function(){
        if(GameConst.IsClickSkin){
            var needAdCnt = GameConst.ClickSkin;
            root.ADgameCnt ++;
            if(root.ADgameCnt >= needAdCnt){
                Laya.timer.once(GameConst.IsEndAdtime,null,function(){
                    platform.showVideoAd(1,'9bf87cbace659524dd11573753137676');
                })
                root.ADgameCnt = 0;
            }
        }
        Laya.SoundManager.playSound("sound/btn.mp3");
        root.hide();
        Shop.show();
    })


    if(User.weaponLevel>=5){
        ui.ad5.visible=true;
    }else{
        ui.ad5.visible=false;
    }
}
return root;
})();
