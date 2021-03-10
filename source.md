-- hutton minimal
-- by donswelt.de

 cartdata("donswelt_huttonminimal") 
 statscargo=dget(0)
 statsdisti=dget(1)
 statsdistf=dget(2)
 
 -- reset statistic
 -- statscargo=0
 -- statsdisti=0
 -- statsdistf=0
 -- dset(0,statscargo)
 -- dset(1,statsdisti)
 -- dset(2,statsdistf)
 
	---------------------------- !

 function _init()

  -- load up the cargo
  cargotype={"craft beer",
       "synthetic meat",
       "tea",
       "coffee",
       "narcotics",
       "gek nip",
       "bootleg liquor",
       "advanced medicines",
       "performance enhancers",
       "synthetic fabrics",
       "biowaste",
       "video games",
       "table top games",
       "sci-fi books",
       "fantasy books",
       "arcade cabinets",
       "pico-8 systems",
       "kakmbul kola",
       "mochi",
       "slurm",
       "cat food",
       "instant ramen",
       "pad krapow",
       "fried rice",
       "fluffy alpacas",
       "short bread",
       "rockforth fertiliser",
       "adorable red panda",
       "90s hiphop vinyl",
       "chili cheese nuggets",
       "old cassette tapes",
       "pizza",
       "collectibles",
       "sam porter bridges",
       "kizuna encounter eu",
       "malt beer",
							"alien eggs",
							"her name is candy",
							"classic movies",
							"percy the rover",
							"ice cream",
							"toilet paper",
							"p.-g. gargle blaster",
							"moloko plus",
							"victory gin",
							"duff beer",
							"blue milk",
							"pitt cola",
							"nuka-cola",
							"empty box",
							"cat litter",
							"kryptonite",
							"starlink satellite",
							"covid vaccine",
							"surgical masks",
							"bfg 9000",
							"cheese cake",
							"tiberium",
							"playstation 5",
							"xbox series s",
							"xbox series x",
							"dreamcast consoles",
							"switch consoles",
							"sentinent robots",
							"betamax tapes",
							"zune players",
							"minidisc players",
							"flux capacitor",
							"sands of time",
							"floppy disks",
							"six golden coins",
							"chainsaw fuel",
							"turbo duo",
							"dry-aged yikyak",
							"flash player",
							"polybius prototype"
							}

  -- what's left to say
  quotes={"    did i    \n  leave the  \n  stove on?  ",
          "    erm.     \n    what     \n    now!?    ",
          "  (should i  \n press this  \n  button!?)  ",
          "    time     \n    for a    \ncoffee break!",
          "    time     \n   to take   \n   a break.  ",
          "    wait,    \n   is that   \n a thargoid? ",
          "    it's     \n  so black   \n  out here.  ",
          "    mum,     \n   are we    \n there yet!? ",
          "remember neo:\n  there is   \n  no spoon!  ",
          "   why am    \n   i doing   \n this again? ",
          " i think the \ncheck engine \n light is on.",
          "   cool,     \n    cool,    \n     cool.   ",
          "this doesn't \n make sense. \n i like it!  ",
          "oh, the cargo\n is smelling \n really good.",
          "   this is   \nsurprisingly \n    easy.    ",
          "  don't fly  \n   without   \n   rebuy!    ",
          "    jump,    \nscoop, jump, \nscoop, repeat",
          " good thing  \ni brought my \n   pico-8.   ",
          "    stay     \n  healthy!   \nwear a mask! ",
          " i once met  \ntwo guys from\n  andromeda. ",
          "this is made \nwith guardian\n    tech!    ",
          "     for     \n     the     \n    mug!     ",
          "i'm here for \n  the free   \n   conda!    ",
          "   space!    \n  the final  \n  frontier!  ",
          "   short,    \n controlled  \n   bursts.   ",
          "    don't    \n    panic,   \n     huh?    ",
          "  doors and  \n   corners,  \n     kid.    ",
          "the stars are\n better off  \n without us. ",
          "  from our   \n  ships, we  \n    live.    ",
          "   by the    \n  stars, we  \n    hope.    ",
          "  live long  \n     and     \n  prosper.   ",        
          "    this     \n     is      \n  the way.   ",
          "    never    \n   tell me   \n  the odds.  ",
          "     i       \n    have     \n   spoken.   ",
          "    fear     \n   is the    \nmind killer. ",
          "the earth is \n  not flat   \n by the way. ",
          "    this     \n     is      \n    fine.    "
         }
        
  stars={}
  for s=1,48 do
   add(stars,summon_star())
  end

  junks={}
  for s=1,6 do
   add(junks,summon_junk())
  end

  titleinit() 

 end

	---------------------------- !

 function _update60()
  if (mode==0) then
   titleupdate()
   elseif (mode==2) then
    endupdate()
   elseif (mode==3) then
    howtoupdate()
   else
    gameupdate()
  end
 end

	---------------------------- !

 function titleupdate()
 
  for star in all(stars) do
   star.x-=star.speed
   if star.x<0 then
    star.x=128
    star.y=rnd(128)
    star.speed=flr(1+rnd(3))
   end
  end
	
	 if btnp(5) then
   howtoinit()
	 end

  i+=1
  if i>=36 then
   i=0
   pressfire+=128
   if pressfire>128 then
    pressfire=0
   end
  end

 end

	---------------------------- !

 function gameupdate()

	 -- finally!
	 if hutton_x<128 and hutton_x>-71 and thrust==0 then
   statscargo+=1
   music(3)
   dset(0,statscargo)
   dset(1,statsdisti)
   dset(2,statsdistf)
   endinit()
	 end

	 -- fullspeed ahead?
	 if thrust==1 then
	  fullspeed()
	 end
	
	 -- we brake for somebody?
	 if thrust==-1 then
	  fullbrake()
	 end
	
	 -- rotate the dish!
	 i+=1
	 if i>=7 then
	  i=0
   dish+=1
   if dish>79 then
	   dish=74
	  end
	 end
 
  -- animate the screen
  if thrust==1 then
   ii+=1
   if ii>1000 then
    screen+=1
    if ii>1007 then
     screen=90
     ii=0
    end
   end
  end
 
  -- the check enginge light
  iii+=1
  if iii>100 then
   iii=0
   light+=1
   if light>105 then
    light=104
   end
  end
 
  -- bla,bla,bla!
  a+=1
  if a==1000 and flr(rnd(2))==0 then
   bubble=0
   quote=flr(rnd(#quotes)+1)
   end
  if a>=1300 then
   a=0
   bubble=128
  end
  
  -- did i left the stove on?
	 if btnp(5) then
	  if thrust==1 then
	   thrust=-1
	   cruising=0
	   sfx(3)
	   music(-1,1)
	  end
	  
	  -- hit fullspeed!
		 if thrust==0 then
	   thrust=1
	   cruising=1
	   music(1)
	   sfx(8)
	  end
	 end
	
	 -- are we there yet!?
	 if cruising==1 then
	  travel-=1
	  if travel<0 then
	   travel=travelfactor
	   distance-=1
	   statsdistf+=1
	    if statsdistf>99 then
	     statsdistf=0
	     statsdisti+=1
	    end
	   dset(1,statsdisti)
	   dset(2,statsdistf)
	   if distance<0 then
	    distance=0
	   end
	   if distance==1 and alert==0 then
	    music(0)
     music(-1,30000)
     alert=1
	   end
	  end
  end
 
 	if hutton_x<-72 and thrust==0 then
   titleinit()
  end
  	
 end

	---------------------------- !

 function endupdate()
  if btnp(5) then
   titleinit()
	 end
 end

	---------------------------- !
	
 function howtoupdate()
 
  for star in all(stars) do
   star.x-=star.speed
 	  if star.x<0 then
 	   star.x=128
 	   star.y=rnd(128)
 	   star.speed=flr(1+rnd(3))
 	  end
  end

  if btnp(5) then
   gameinit()
	 end
	
	 i+=1
   if i>=36 then
    i=0
    pressfire+=128
     if pressfire>128 then
      pressfire=0
     end
   end
 
 end
	
	---------------------------- !

 function _draw()
  if (mode==0) then
    titledraw()
  elseif (mode==2) then
    enddraw()
  elseif (mode==3) then
    howtodraw()
  else
    gamedraw()
  end
 end

	---------------------------- !

 function titledraw()
	 cls()
	 
	 if statsdistf <10 then
	  statsdistfz="0"..statsdistf
	 else
	  statsdistfz=statsdistf
	 end
	  
  for star in all(stars) do
   pset(star.x,star.y,15)
  end

  map(0,10,31,7,8,4)
 
  print("an elite demake",hcenter("an elite demake"),43,9)
  print("total units of",hcenter("total units of"),58,12)
  print("cargo delivered: "..statscargo.."",hcenter("cargo delivered: "..statscargo..""),65,12)
  print("total distance",hcenter("total distance"),75,12)
  print("travelled: "..statsdisti.."."..statsdistfz.." ly",hcenter("travelled: "..statsdisti.."."..statsdistfz.." ly"),82,12)

  print("press ❎ to start",hcenter("press ❎ to start")-2,100+pressfire,9)
  print("2021 ♥ donswelt.de",hcenter("2021 ♥ donswelt.de")-2,117,12) 
 
 end

	---------------------------- !

 function gamedraw()

  -- draw things
  cls()
 
  -- stars in background
  for star in all(stars) do
   pset(star.x,star.y,15)
  end

  -- hutton minimal \o/
	 map(7,0,hutton_x,36,18,10,0)
	
	 -- the ship
	 map(0,0,32,50,7,5,0)
  rect(37,68,37,78,14)
 
  -- the dish
  spr(dish,56,50)
 
  -- the screen
  spr(screen,64,66)
 
  -- the light
  spr(light,62,80)
 
  -- space junk
  for junk in all(junks) do
 	 spr(junk.rnjunk,junk.x,junk.y)
	 end
	
  -- the osd
	 print("distance to",hcenter("distance to"),5,12)
	 print("hutton minimal: 0."..distance.." ly",hcenter("hutton minimal: 0."..distance.." ly"),13,12)
	 print("cargo: "..cargo,hcenter("cargo: "..cargo),118,12)

	 -- erm, you missed the exit
	 if hutton_x<-72 then
   print("you missed",hcenter("you missed"),30,8)
   print("hutton minimal",hcenter("hutton minimal"),38,8)
	 end
	
 	-- bla,bla,bla!
	 map(0,14,55,24+bubble,8,17)
	 print(quotes[quote],61,27+bubble,1)
 end

	---------------------------- !

 function enddraw()
	 print("welcome to",hcenter("welcome to"),24,9)
	 print("hutton minimal!",hcenter("hutton minimal!"),32,9)
 end
 
 ---------------------------- !
 
 function howtodraw()
  cls()
 
  for star in all(stars) do
   pset(star.x,star.y,15)
  end
 
  map(8,10,19,15,17,18)
  print("you are a space\ntrucker and all\nyou need to do\nis fly to\nhutton minimal\nand deliver your\ncargo. it's a\nlong way.\n\ncontrols:\n❎ to turn\nthrusters on/off",32,23,7)
 
  print("press ❎ to continue",hcenter("press ❎ to continue")-2,110+pressfire,9)
  print("v1.0",109,119,1)
 	
 end
 
	-------- functions --------- !
 
 -- how about stars?
 function summon_star()
	 local star={
	 x=flr(rnd(128)),
	 y=flr(rnd(128)),
	 speed=flr(1+rnd(3)),
	 }
	 return star
 end
 
 -- how about some junk?
 function summon_junk()
	 local junk={
	 x=flr(rnd(10000))+128,
		y=rnd(110),
		rnjunk=57+flr(rnd(6))
	 }
	 return junk
 end

 -- fullspeed ahead!
 function fullspeed()
  pal(14,rnd(16))
  timer+=1
   if timer>maxthrust then
   timer=0
    if maxthrust>0 then
    maxthrust-=1
    end
   
    -- move hutton
    if distance==0 and hutton_x>-100 then
     hutton_x-=1
    end

    -- move the stars
    for star in all(stars) do
     if thrust==1 then
 			  star.x-=star.speed
 	 		 if star.x<0 then
 	  		 star.x=128
 	  		 star.y=rnd(128)
 	  		 star.speed=flr(1+rnd(3))
 	 		 end
     end
    end

    -- move the junk
    for junk in all(junks) do
     if thrust==1 then
      junk.x-=1
      if junk.x<-20 then
    		 junk.x=flr(rnd(10000))+128
    		 junk.y=rnd(110)
    		 junk.rnjunk=57+flr(rnd(6))
      end
     end
    end	
	  
	 end
 end

 function fullbrake()
  pal(14,0)
  timer+=1
   if timer>maxthrust then
    timer=0
    maxthrust+=1
     if maxthrust>20 then
      maxthrust=20
      thrust=0
      music(-1)
     end

     -- move hutton
     if distance==0 and hutton_x>-100 then
      hutton_x-=1
     end

     for star in all(stars) do
      if thrust==-1 then
       star.x-=star.speed
        if star.x<0 then
         star.x=128
         star.y=flr(rnd(128))
        end
      end
     end
     
				-- move the junk
    for junk in all(junks) do
     if thrust==-1 then
      junk.x-=1
       if junk.x<-20 then
    		  junk.x=flr(rnd(10000))+128
    		  junk.y=rnd(110)
    		  junk.rnjunk=57+flr(rnd(6))
       end
     end
    end	

 end
end

 function titleinit()
  mode=0
  timer=0
  speed=0
  thrust=0
  cruising=0
  maxthrust=20
  distance=22
  travelfactor=2000
  travel=travelfactor
  hutton_x=128
  station_x=-128
  alert=0
  rnjunk=56
  lypos=87
  a=0
  i=0
  ii=0
  iii=0
  dish=74
  screen=90
  light=104
  pressfire=0
  bubble=128
  quote=0
  cargo=cargotype[flr(rnd(#cargotype))+1]
  cargoweight=flr(rnd(8))+1
  pal(14,0)
  music(3)
 end

 function gameinit()
  mode=1
  music(-1,3000)
 end

 function endinit()
  mode=2
 end

 function howtoinit()
  mode=3
 end

 function hcenter(s)
  -- screen center minus the
  -- string length times the 
  -- pixels in a char's width,
  -- cut in half
  return 64-#s*2
 end
