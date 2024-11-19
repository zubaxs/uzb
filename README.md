<?php
ob_start();
error_reporting(0);
date_Default_timezone_set('Asia/Tashkent');

define('API_KEY',"7228076051:AAHQMYfq-D24a7_f3uyPhz66UIlHQWmlLsg");//Token yozasiz

$shakh_akn = "972211627";//asosiy admin
$admin = array("$shakh_akn","972211627","id");//adminlar
$bot = bot('getme',['bot'])->result->username;


function bot($method,$datas=[]){
$url = "https://api.telegram.org/bot".API_KEY."/".$method;
$ch = curl_init();
curl_setopt($ch,CURLOPT_URL,$url);
curl_setopt($ch,CURLOPT_RETURNTRANSFER,true);
curl_setopt($ch,CURLOPT_POSTFIELDS,$datas);
$res = curl_exec($ch);
if(curl_error($ch)){
var_dump(curl_error($ch));
}else{
return json_decode($res);
}}

$kanallar=file_get_contents("channel.txt");
function joinchat($id){
global $mid;
$array = array("inline_keyboard");
$kanallar=file_get_contents("channel.txt");
if($kanallar == null){
return true;
}else{
$ex = explode("\n",$kanallar);
for($i=0;$i<=count($ex) -1;$i++){
$first_line = $ex[$i];
$first_ex = explode("@",$first_line);
$url = $first_ex[1];
$ism=bot('getChat',['chat_id'=>"@".$url,])->result->title;
$ret = bot("getChatMember",[
"chat_id"=>"@$url",
"user_id"=>$id,
]);
$stat = $ret->result->status;
if((($stat=="creator" or $stat=="administrator" or $stat=="member"))){
$array['inline_keyboard']["$i"][0]['text'] = "✅ ". $ism;
$array['inline_keyboard']["$i"][0]['url'] = "https://t.me/$url";
}else{
$array['inline_keyboard']["$i"][0]['text'] = "❌ ". $ism;
$array['inline_keyboard']["$i"][0]['url'] = "https://t.me/$url";
$uns = true;
}
}
$array['inline_keyboard']["$i"][0]['text'] = "🔄 Tekshirish";
$array['inline_keyboard']["$i"][0]['url'] = "https://t.me/$bot?start=$cid2";
if($uns == true){
bot('sendMessage',[
'chat_id'=>$id,
'text'=>"<b>⚠️ Botdan to'liq foydalanish uchun quyidagi kanallarimizga obuna bo'ling!</b>",
'parse_mode'=>'html',
'disable_web_page_preview'=>true,
'reply_markup'=>json_encode($array),
]);
return false;
}else{
return true;
}}}

$servername = "localhost";
$username = "nomi"; //mysql baza nomi
$password = "paroli"; //mysql baza paroli
$connect = new mysqli($servername, $username, $password, $username);

if($connect){
    echo "Ulandi";
}else{
    echo "Ulanmadi $connect->error";
}


mysqli_query($connect,"CREATE TABLE `users` (
  `users_id` int(11) NOT NULL AUTO_INCREMENT,
  `user_id` text NOT NULL,
  `holat` text NOT NULL,
  `vaqt` text NOT NULL,
  PRIMARY KEY (`users_id`)
)");


mysqli_query($connect,"CREATE TABLE `yoqtirishlar` (
  `like_id` int(11) NOT NULL AUTO_INCREMENT,
`user_id` text NOT NULL,
`nomi` text NOT NULL,
 `davlati` text NOT NULL,
 `formati` text NOT NULL,
 `janri` text NOT NULL,
 `yili` text NOT NULL,
 `tili` text NOT NULL,
 `haqida` text NOT NULL,
 `rasm_id` text NOT NULL,
 `video_id` text NOT NULL,
  PRIMARY KEY (`like_id`)
)");


mysqli_query($connect,"CREATE TABLE `kinolar` (
  `kino_ids` int(11) NOT NULL AUTO_INCREMENT,
`nomi` text NOT NULL,
 `davlati` text NOT NULL,
 `formati` text NOT NULL,
 `janri` text NOT NULL,
 `yili` text NOT NULL,
 `tili` text NOT NULL,
 `haqida` text NOT NULL,
 `rasm_id` text NOT NULL,
 `video_id` text NOT NULL,
  PRIMARY KEY (`kino_ids`)
)");




///Avto Webhook!
$a=file_get_contents("https://api.telegram.org/bot".API_KEY."/setwebhook?url=".$_SERVER['SERVER_NAME']."".$_SERVER['SCRIPT_NAME']);
echo $a;
//

$update = json_decode(file_get_contents('php://input'));
$message = $update->message;
$cid = $message->chat->id;
$name = $message->chat->first_name;
$tx = $message->text;
$step = file_get_contents("step/$cid.step");
$mid = $message->message_id;
$type = $message->chat->type;
$text = $message->text;
$uid= $message->from->id;
$name = $message->from->first_name;
$familya = $message->from->last_name;
$bio = $message->from->about;
$username = $message->from->username;
$chat_id = $message->chat->id;
$message_id = $message->message_id;
$reply = $message->reply_to_message->text;
$nameru = "<a href='tg://user?id=$uid'>$name $familya</a>";

$botdel = $update->my_chat_member->new_chat_member; 
$botdelid = $update->my_chat_member->from->id; 
$userstatus= $botdel->status; 

$contact = $message->contact;
$contact_id = $contact->user_id;
$contact_user = $contact->username;
$contact_name = $contact->first_name;
$phone = $contact->phone_number;


//inline uchun metodlar
$data = $update->callback_query->data;
$qid = $update->callback_query->id;
$id = $update->inline_query->id;
$query = $update->inline_query->query;
$query_id = $update->inline_query->from->id;
$cid2 = $update->callback_query->message->chat->id;
$mid2 = $update->callback_query->message->message_id;
$callfrid = $update->callback_query->from->id;
$callname = $update->callback_query->from->first_name;
$calluser = $update->callback_query->from->username;
$surname = $update->callback_query->from->last_name;
$about = $update->callback_query->from->about;
$nameuz = "<a href='tg://user?id=$callfrid'>$callname $surname</a>";

$photo = $message->photo;
$file = $photo[count($photo)-1]->file_id;


mkdir("step");

$test1 = file_get_contents("step/test1.txt");
$test2 = file_get_contents("step/test2.txt");
$test3 = file_get_contents("step/test3.txt");
$test4 = file_get_contents("step/test4.txt");
$test5 = file_get_contents("step/test5.txt");
$test6 = file_get_contents("step/test6.txt");
$test7 = file_get_contents("step/test7.txt");
$test8 = file_get_contents("step/test8.txt");



if(file_get_contents("kino_ch.txt")){
	}else{
		if(file_put_contents("kino_ch.txt","@Education_PHP"));
}
if(file_get_contents("holat.txt")){
	}else{
		if(file_put_contents("holat.txt","Yoqilgan"));
}

if($botdel){ 
if($userstatus=="kicked"){ 
mysqli_query($connect,"UPDATE users SET holat = '❌' WHERE user_id = $botdelid");
}}
if(isset($message)){
mysqli_query($connect,"UPDATE users SET holat = '✅' WHERE user_id = $cid");
}



$umum_d = date("d.m.Y H:i");
if(isset($message)){
$result = mysqli_query($connect,"SELECT * FROM users WHERE user_id = $cid");
$row = mysqli_fetch_assoc($result);
if(!$row){
mysqli_query($connect,"INSERT INTO users(`user_id`,`holat`,`vaqt`) VALUES ('$cid','✅','$umum_d')");
}
}

$kanal_uz = file_get_contents("step/kanal.txt");
$kanalcha = file_get_contents("kino_ch.txt");
$holat = file_get_contents("holat.txt");

if($data == "yoqot"){
bot('deleteMessage',[
        'chat_id'=>$cid2,
       'message_id'=>$mid2,
]);
bot('SendMessage',[
'chat_id'=>$cid2,
'text'=>"<b>🖥 Asosiy menyuga qaytdingiz</b>",
'parse_mode'=>'html',
'reply_markup'=>$menu,
]);
bot('deleteMessage',[
'chat_id'=>$cid,
'message_id'=>$del,
]);
exit();
}

$menu = json_encode([
'resize_keyboard'=>true,
'keyboard'=>[
[['text'=>"🔎 Kinolarni qidirish"]],
[['text'=>"❤️ Yoqtirishlar"],['text'=>"☎️ Admin"]],
]
]);

$panel = json_encode([
'resize_keyboard'=>true,
'keyboard'=>[
[['text'=>"📢 Kanallarni sozlash"]],
[['text'=>"📊 Statistika"],['text'=>"✉ Xabar Yuborish"]],
[['text'=>"📤 Kino Yuklash"]],
[['text'=>"🤖 Bot holati"],['text'=>"◀️ Orqaga"]],
]
]);

$back = json_encode([
'resize_keyboard'=>true,
'keyboard'=>[
[['text'=>"◀️ Orqaga"]],
]
]);

$boshqarish = json_encode([
'resize_keyboard'=>true,
'keyboard'=>[
[['text'=>"🗄 Boshqarish"]],
]
]);

$holat = file_get_contents("holat.txt");
if($text){
 if($holat == "O'chirilgan"){
	if(in_array($cid,$admin)){
}else{
	bot('sendMessage',[
	'chat_id'=>$cid,
	'text'=>"⛔️ <b>Bot vaqtinchalik o'chirilgan!</b>

<i>Botda ta'mirlash ishlari olib borilayotgan bo'lishi mumkin!</i>",
'parse_mode'=>'html',
]);
exit();
}
}
}

if($data){
 if($holat == "O'chirilgan"){
	if(in_array($cid2,$admin)){
}else{
	bot('answerCallbackQuery',[
		'callback_query_id'=>$qid,
		'text'=>"⛔️ Bot vaqtinchalik o'chirilgan!

Botda ta'mirlash ishlari olib borilayotgan bo'lishi mumkin!",
		'show_alert'=>true,
		]);
exit();
}
}
}

if($text == "/start" and joinchat($cid) == true){	
	bot('SendMessage',[
	'chat_id'=>$cid,
	'text'=>"🖥️ Asosiy menyudasiz:

Kino kodlar: $kanalcha",
	'parse_mode'=>'html',
'disable_web_page_preview'=>true,
	'reply_markup'=>$menu
	]);
exit();
   unlink("step/test1.txt");
   unlink("step/test2.txt");
   unlink("step/test3.txt");
   unlink("step/test4.txt");
   unlink("step/test5.txt");
   unlink("step/test6.txt");
   unlink("step/test7.txt");
   unlink("step/test8.txt");
}

if($text == "◀️ Orqaga" and joinchat($cid) == true){        
	bot('SendMessage',[
	'chat_id'=>$cid,
	'text'=>"<b>🖥 Asosiy menyuga qaytdingiz.

🔎 Kinolarni qidirish: $kanalcha</b>",
	'parse_mode'=>'html',
	'reply_markup'=>$menu,
]);
unlink("step/$cid.step");
   unlink("step/test1.txt");
   unlink("step/test2.txt");
   unlink("step/test3.txt");
   unlink("step/test4.txt");
   unlink("step/test5.txt");
   unlink("step/test6.txt");
   unlink("step/test7.txt");
   unlink("step/test8.txt");
exit();
}


if($text == "🔎 Kinolarni qidirish"){
	bot('SendMessage',[
	'chat_id'=>$cid,
	'text'=>"👋 <b>Marhamat, quyidagilardan birini tanlang:</b>",
	'parse_mode'=>'html',
	'reply_markup'=>json_encode([
	'inline_keyboard'=>[
	[['text'=>"🔎 Kod kiritish",'callback_data'=>"yukla"]],
	[['text'=>"🔄 Tasodifiy kino",'callback_data'=>"tasodif"]],
]
])
	]);
exit();
}

if($data == "yukla"){
	bot('deleteMessage',[
'chat_id'=>$cid2,
'message_id'=>$mid2,
]);
	bot('sendmessage',[
	'chat_id'=>$cid2,
	'text'=>"<b>Marhamat, kerakli kodni yuboring:</b>",
	'parse_mode'=>'html',
	'reply_markup'=>$back,
	]);
	file_put_contents("step/$cid2.step",'kinoids');
	exit();
}

if($data == "tasodif"){
$res = mysqli_query($connect, "SELECT * FROM `kinolar`");
$a = mysqli_num_rows($res);
$b = rand(1,$a);
if($a != null){
	$res = mysqli_query($connect,"SELECT*FROM kinolar WHERE kino_ids = '$b'");
while($a = mysqli_fetch_assoc($res)){
$name = $a['nomi'];
$janri = $a['janri'];
$haqida = $a['haqida'];
$langs = $a['tili'];
$formats = $a['formati'];
$countrs = $a['davlati'];
$year = $a['yili'];
$rasmii = $a['rasm_id'];
$file_id = $a['video_id'];
}
bot('deleteMessage',[
'chat_id'=>$cid2,
'message_id'=>$mid2,
]);
bot('sendVideo',[
'chat_id'=>$cid2,
'video'=>$file_id,
'caption'=>"<b>🎬 Nomi: $name

🧨 $haqida

🌎 Davlati: $countrs 
💽 Formati: $formats
🇺🇿 Tili: $langs
#⃣ Janri: $janri
🗓 Yili: $year

🟥 Kino kodi: <code>$b</code></b>",
'parse_mode'=>'html',
'reply_markup'=>json_encode([
'inline_keyboard'=>[
[['text'=>"🔄 Tasodifiy kino",'callback_data'=>"tasodif"]],
[['text'=>"🖇️ Filmni ulashish",'url'=>"https://t.me/share/url?url=https://t.me/$bot?start=$b"]],
]
])
]);
}else{
bot('answerCallbackQuery',[
'callback_query_id'=>$qid,
'text'=>"🤷🏼‍♂️ Tasodifiy kinolar topilmadi!",
'show_alert'=>false
]);
}
}

if($step == "kinoids"){
	$res = mysqli_query($connect,"SELECT*FROM kinolar WHERE kino_ids = '$text'");
while($a = mysqli_fetch_assoc($res)){
$name = $a['nomi'];
$janri = $a['janri'];
$haqida = $a['haqida'];
$langs = $a['tili'];
$formats = $a['formati'];
$countrs = $a['davlati'];
$year = $a['yili'];
$rasmii = $a['rasm_id'];
}
$result = mysqli_query($connect,"SELECT * FROM kinolar WHERE kino_ids = '$text'");
$row = mysqli_fetch_assoc($result);
if(!$row){
bot('SendMessage',[
	'chat_id'=>$cid,
	'text'=>"<b>Kino topilmadi.</b>

Qayta urinib ko'ring:",
'parse_mode'=>'html',
]);
exit();
}else{
bot('SendPhoto',[
      'chat_id'=>$cid,
     'photo'=>$rasmii,
'caption'=>"<b>🎬 Nomi: $name

🧨 $haqida

🌎 Davlati: $countrs 
💽 Formati: $formats
🇺🇿 Tili: $langs
#⃣ Janri: $janri
🗓 Yili: $year

🟥 Kino kodi: <code>$text</code></b>",
'parse_mode'=>'html',
'reply_markup'=>json_encode([
	'inline_keyboard'=>[
[['text'=>"❤️ Yoqtirish",'callback_data'=>"like=$text"],['text'=>"📥 Yuklash",'callback_data'=>"saqlash1=$text"]],
[['text'=>"🖇️ Filmni ulashish",'url'=>"https://t.me/share/url?url=https://t.me/$bot?start=$text"]],
]
])
]);
unlink("step/$cid.step");
exit();
}
}

if(mb_stripos($data,"saqlash1=")!==false){
$ex = explode("=",$data);
$eex = $ex[1];
$name = mysqli_fetch_assoc(mysqli_query($connect,"SELECT*FROM kinolar WHERE kino_ids = $eex"))['nomi'];
$file = mysqli_fetch_assoc(mysqli_query($connect,"SELECT*FROM kinolar WHERE kino_ids = $eex"))['video_id'];
bot('deleteMessage',[
'chat_id'=>$cid2,
'message_id'=>$mid2,
]);
bot("SendVideo", [
"chat_id"=>$cid2,
'video'=>$file,
'caption'=>"📄: $name

📥 Kino muvaffaqiyatli yuklandi...",
"parse_mode" => "html",
]);
}

if(mb_stripos($data,"like=")!==false){
$ex = explode("=",$data);
$exe = $ex[1];
$res = mysqli_query($connect,"SELECT*FROM kinolar WHERE kino_ids = '$exe'");
while($a = mysqli_fetch_assoc($res)){
$name = $a['nomi'];
$janri = $a['janri'];
$haqida = $a['haqida'];
$langs = $a['tili'];
$formats = $a['formati'];
$countrs = $a['davlati'];
$year = $a['yili'];
$rasmii = $a['rasm_id'];
$kodi = $a['video_id'];
}
mysqli_query($connect, "INSERT INTO `yoqtirishlar`(`user_id`,`nomi`,`davlati`,`formati`,`janri`,`yili`,`tili`,`haqida`,`rasm_id`,`video_id`) VALUES ('$cid2','$name','$countrs','$formats','$janri','$year','$langs','$haqida','$rasmii','$kodi')");
bot('deleteMessage',[
'chat_id'=>$cid2,
'message_id'=>$mid2,
]);
bot('sendMessage',[
'chat_id'=>$cid2,
'text'=>"<b>❤️ Bu kino sizga yoqdi</b>",
'disable_web_page_preview'=>true,
'parse_mode'=>'html',
'reply_markup'=>$back,
]);
}



if($text == "☎️ Admin" and joinchat($cid) == true){	
	bot('SendMessage',[
	'chat_id'=>$cid,
	'text'=>"📑Savol va Takliflar bo'lsa @shakh_akn profiliga muroojat qilishingiz mumkin!",
	'parse_mode'=>'html',
'disable_web_page_preview'=>true,
	'reply_markup'=>$menu
	]);
exit();
}

if($text == "❤️ Yoqtirishlar" and joinchat($cid) == true){
$key = [];
$sql = mysqli_query($connect, "SELECT * FROM `yoqtirishlar` WHERE `user_id` = '$cid'");
while($us = mysqli_fetch_assoc($sql)){
$user = $us['nomi'];
$ids = $us['like_id'];
$key[] = ["text"=>"📥 $user","callback_data"=>"bought:$ids"];
}
$keyboard2 = array_chunk($key, 1);
$keyboard2[] = [['text'=>"🏡 Bosh sahifa",'callback_data'=>"yoqot"],['text'=>"🗑️ Tozalash",'callback_data'=>"tozalash"]];
$bolim = json_encode([
'inline_keyboard'=>$keyboard2
]);
$result = mysqli_query($connect, "SELECT * FROM `yoqtirishlar`");
$row = mysqli_fetch_assoc($result);
if($row){
bot('deleteMessage',[
'chat_id'=>$cid,
'message_id'=>$del,
]);
$del = bot('sendMessage', [
'chat_id'=>$cid,
'text'=>"<b>Kuting...</b>",
'parse_mode'=>'html',
'reply_markup'=>json_encode([
'remove_keyboard'=>true
])
])->result->message_id;
sleep(0.1);
bot('deleteMessage',[
'chat_id'=>$cid,
'message_id'=>$del,
]);
bot('sendMessage',[
'chat_id'=>$cid,
'text'=>"<b>⏬ Quyidagilardan birini tanlang.</b>",
'parse_mode'=>'html',
'reply_markup'=>$bolim,
]);
exit();
}else{
bot('sendMessage',[
'chat_id'=>$cid,
'text'=>"<b>🤷‍♂️ Hech qanday maʼlumot topilmadi...</b>",
'parse_mode'=>'html',
'reply_markup'=>$menu,
]);
exit();
}
}



if($data == "tozalash"){
	bot('deleteMessage',[
	'chat_id'=>$cid2,
	'message_id'=>$mid2,
	]);
	mysqli_query($connect, "DELETE FROM `yoqtirishlar` WHERE `user_id` = '$cid2'");
	bot('SendMessage',[
	'chat_id'=>$cid2,
'text'=>"<b>✅️ Yoqtirishlat tozalandi....</b>",
'parse_mode'=>'html',
'reply_markup'=>$menu,
]);
}

if(mb_stripos($data,"bought:")!==false){
$ex = explode("bought:",$data);
$exe = $ex[1];
$res = mysqli_query($connect,"SELECT*FROM yoqtirishlar WHERE like_id = '$exe'");
while($a = mysqli_fetch_assoc($res)){
$name = $a['nomi'];
$janri = $a['janri'];
$haqida = $a['haqida'];
$langs = $a['tili'];
$formats = $a['formati'];
$countrs = $a['davlati'];
$year = $a['yili'];
$rasmii = $a['rasm_id'];
}
bot('deleteMessage',[
'chat_id'=>$cid2,
'message_id'=>$mid2,
]);
bot('sendphoto',[
'chat_id'=>$cid2,
'photo'=>$rasmii,
'caption'=>"<b>🎬 Nomi: $name

🧨 $haqida

🌎 Davlati: $countrs 
💽 Formati: $formats
🇺🇿 Tili: $langs
#⃣ Janri: $janri
🗓 Yili: $year</b>",
'disable_web_page_preview'=>true,
'parse_mode'=>'html',
'reply_markup'=>json_encode([
'inline_keyboard'=>[
[['text'=>"🎥 Kinoni yuklab olish",'callback_data'=>"saqlash-$exe"]],
[['text'=>"🏡",'callback_data'=>"yoqot"]],
]
])
]);
}


if(mb_stripos($data,"saqlash-")!==false){
$ex = explode("-",$data);
$ex = $ex[1];
$name = mysqli_fetch_assoc(mysqli_query($connect,"SELECT*FROM yoqtirishlar WHERE like_id = $ex"))['nomi'];
$file = mysqli_fetch_assoc(mysqli_query($connect,"SELECT*FROM yoqtirishlar WHERE like_id = $ex"))['video_id'];
bot('deleteMessage',[
	'chat_id'=>$cid2,
	'message_id'=>$mid2,
	]);
bot("SendVideo", [
"chat_id"=>$cid2,
'video'=>$file,
'caption'=>"📄: $name

📥 Kino muvaffaqiyatli yuklandi...",
"parse_mode" => "html",
'reply_markup'=>$menu,
]);
}


if($text == "🗄 Boshqarish" or $text=="/panel"){
	if(in_array($cid,$admin)){
	bot('SendMessage',[
	'chat_id'=>$cid,
	'text'=>"<b>Admin paneliga xush kelibsiz!</b>",
	'parse_mode'=>'html',
	'reply_markup'=>$panel,
	]);
	unlink("step/$cid.step");
   unlink("step/test.txt");
   unlink("step/$cid.txt");
	exit();
}
}

if($data == "boshqarish"){
	bot('deleteMessage',[
	'chat_id'=>$cid2,
	'message_id'=>$mid2,
	]);
	bot('SendMessage',[
	'chat_id'=>$cid2,
	'text'=>"<b>Admin paneliga xush kelibsiz!</b>",
	'parse_mode'=>'html',
	'reply_markup'=>$panel,
	]);
	exit();
}


if($text == "📢 Kanallarni sozlash"){
	if(in_array($cid,$admin)){
	bot('SendMessage',[
	'chat_id'=>$cid,
	'text'=>"<b>Quyidagilardan birini tanlang:</b>",
	'parse_mode'=>'html',
	'reply_markup'=>json_encode([
	'inline_keyboard'=>[
	[['text'=>"➕ Kanal Qo'shish",'callback_data'=>"kqosh"],['text'=>"🗑 Kanallarni O'chirish",'callback_data'=>"kochir"]],
	[['text'=>"📑 Kanallar Ro'yxat",'callback_data'=>"mroyxat"]],
	]
	])
	]);
	exit();
}
}

/*Kanal obuna bo'lish*/
if($data == "kqosh"){
	if($text=="/start"){
unlink("step/$cid.step");
}else{
bot('editMessagetext',[
'chat_id'=>$cid2,
	'message_id'=>$mid2,
'text'=>"*📢 Kerakli kanalni manzilini yuboring:

Namuna: @LiveBuildersNews*",
'parse_mode'=>'MarkDown',
'reply_markup'=>$back1
]);
file_put_contents("step/$cid2.step",'qosh');
}}

if($step == "qosh"){
if($text=="/start"){
unlink("step/$cid.step");
}else{
if(stripos($text,"@")!==false){
if($kanallar == null){
file_put_contents("channel.txt",$text);
bot('SendMessage',[
'chat_id'=>$cid,
'text'=>"<b>$text - kanal qo'shildi</b>",
'parse_mode'=>'html',
'reply_markup'=>$panel,
]);
unlink("step/$cid.step");
}else{
file_put_contents("channel.txt","$kanallar\n$text");
bot('SendMessage',[
'chat_id'=>$cid,
'text'=>"<b>$text - kanal qo'shildi</b>",
'parse_mode'=>'html',
'reply_markup'=>$panel,
]);
unlink("step/$cid.step");
}}else{
bot('SendMessage',[
'chat_id'=>$cid,
'text'=>"<b>⚠️ Kanal manzili kiritishda xatolik:</b>

Masalan: @LiveBuildersNews",
'parse_mode'=>'html',
]);
}}}

if($data=="kochir"){
bot('deleteMessage',[
'chat_id'=>$cid2,
'message_id'=>$mid2,
]);
bot('sendMessage',[
'chat_id'=>$cid2,
'text'=>"<b>🗑 Kanallar o'chirildi!</b>",
'parse_mode'=>"html",
]);
unlink("channel.txt");
}

if($data=="mroyxat"){
if($kanallar==null){
bot('deleteMessage',[
'chat_id'=>$cid2,
'message_id'=>$mid2,
]);
bot('sendMessage',[
'chat_id'=>$cid2,
'text'=>"<b>Kanallar ulanmagan!</b>",
'parse_mode'=>"html",
'reply_markup'=>json_encode([
'inline_keyboard'=>[
[['text'=>"🏡 Bosh menyu",'callback_data'=>"profil"],['text'=>"◀️ Orqaga",'callback_data'=>"panel"]],
]])
]);
}else{
$soni = substr_count($kanallar,"@");
bot('editMessageText',[
'chat_id'=>$cid2,
'message_id'=>$mid2,
'text'=>"<b>Ulangan kanallar ro'yxati ⤵️</b>
➖➖➖➖➖➖➖➖

<i>$kanallar</i>

<b>Ulangan kanallar soni:</b> $soni ta",
'parse_mode'=>"html",
'reply_markup'=>json_encode([
'inline_keyboard'=>[
[['text'=>"🏡 Bosh menyu",'callback_data'=>"profil"],['text'=>"◀️ Orqaga",'callback_data'=>"panel"]],
]])
]);
}}

if($text == "📊 Statistika"){
	if(in_array($cid,$admin)){
$res = mysqli_query($connect, "SELECT * FROM `users`");
$stat = mysqli_num_rows($res);
$start_time = round(microtime(true) * 1000);
bot('SendMessage',[
'chat_id'=>$cid,
'text'=>"",
'parse_mode'=>'html',
]);
$end_time = round(microtime(true) * 1000);
$ping = $end_time - $start_time;
bot('SendMessage',[
'chat_id'=>$cid,
'text'=>"💡 <b>O'rtacha yuklanish:</b> <code>$ping</code>

👥 <b>Foydalanuvchilar:</b> $stat ta",
'parse_mode'=>'html',
	'reply_markup'=>json_encode([
	'inline_keyboard'=>[
[['text'=>"Orqaga",'callback_data'=>"boshqarish"]]
]
])
]);
exit();
}
}



if($text == "✉ Xabar Yuborish"){
if(in_array($cid,$admin)){
	bot('SendMessage',[
	'chat_id'=>$cid,
	'text'=>"<b>Yuboriladigan xabar turini tanlang:</b>",
	'parse_mode'=>'html',
	'reply_markup'=>json_encode([
	'inline_keyboard'=>[
	[['text'=>"👤 Userga",'callback_data'=>"user"]],
	[['text'=>"🗣️ Oddiy",'callback_data'=>"send"]],
  [['text'=>"Orqaga",'callback_data'=>"boshqarish"]],	
	]
	])
	]);
	exit();
}
}

if($data == "user"){
bot('deleteMessage',[
'chat_id'=>$cid2,
'message_id'=>$mid2,
]);
bot('SendMessage',[
'chat_id'=>$cid2,
'text'=>"<b>Foydalanuvchi iD raqamini kiriting:</b>",
'parse_mode'=>'html',
'reply_markup'=>$boshqarish,
]);
file_put_contents("step/$cid2.step",'user');
exit();
}

if($step == "user"){
if(in_array($cid,$admin)){
if(is_numeric($text)=="true"){
	bot('SendMessage',[
	'chat_id'=>$cid,
	'text'=>"<b>Foydalanuvchiga yubormoqchi bo'lgan xabaringizni kiriting:</b>",
	'parse_mode'=>'html',
	]);
file_put_contents("step/$cid.step","xabar-$text");
exit();
}else{
bot('SendMessage',[
'chat_id'=>$cid,
'text'=>"<b>Faqat raqamlardan foydalaning!</b>",
'parse_mode'=>'html',
]);
exit();
}
}
}

if(mb_stripos($step, "xabar-") !== false){
if(in_array($cid,$admin)){
$id = explode("-", $step)[1];
$get = bot('getChat',[
'chat_id'=>$id,
]);
$first = $get->result->first_name;
$users = $get->result->username;
$pul = mysqli_fetch_assoc(mysqli_query($connect,"SELECT*FROM users WHERE user_id=$id"))['balance'];
$odam = mysqli_fetch_assoc(mysqli_query($connect,"SELECT*FROM users WHERE user_id = $id"))['referal'];
	bot('SendMessage',[
	'chat_id'=>$id,
	'text'=>"$text",
        'parse_mode'=>'html',
'disable_web_page_preview'=>true,
	]);
	bot('SendMessage',[
	'chat_id'=>$cid,
	'text'=>"✅ <b>Foydalanuvchiga xabaringiz yuborildi!</b>",
       'parse_mode'=>'html',
        'reply_markup'=>$panel,
	]);
	unlink("step/$cid.step");
	exit();
}
}



if($data == "send"){
bot('deleteMessage',[
'chat_id'=>$cid2,
'message_id'=>$mid2,
]);
bot('SendMessage',[
'chat_id'=>$cid2,
    'text'=>"*Xabar matnini kiriting:*",
'parse_mode'=>'MarkDown',
'reply_markup'=>$boshqarish,
    ]);
file_put_contents("step/$cid2.step","sendpost");
exit();
}

if($step == "sendpost"){
if(in_array($chat_id,$admin)){
  unlink("step/$chat_id.step");
$res = mysqli_query($connect,"SELECT * FROM `users`");
bot('sendMessage',[
  'chat_id'=>$chat_id,
  'text'=>"*Xabar Yuborish Boshlandi* ✅",
'parse_mode'=>'MarkDown',
  ]);
$x=0;
$y=0;
while($a = mysqli_fetch_assoc($res)){
$id = $a['user_id'];
	$key=$message->reply_markup;
	$keyboard=json_encode($key);
	$ok=bot('copyMessage',[
'from_chat_id'=>$chat_id,
'chat_id'=>$id,
'message_id'=>$mid,
])->ok;
if($ok==true){
}else{
$okk=bot('copyMessage',[
'from_chat_id'=>$chat_id,
'chat_id'=>$id,
'message_id'=>$mid,
])->ok;
}
if($okk==true or $ok==true){
$x=$x+1;
bot('editMessageText',[
  'chat_id'=>$chat_id,
'message_id'=>$mid,
'text'=>"✅ <b>Yuborildi:</b> $x

❌ <b>Yuborilmadi:</b> $y",
'parse_mode'=>'html',
'reply_markup'=>$panel
]);
}elseif($okk==false){
$y=$y+1;
bot('editmessagetext',[
'chat_id'=>$chat_id,
'message_id'=>$mid + 1,
'text'=>"✅ <b>Yuborildi:</b> $x

❌ <b>Yuborilmadi:</b> $y",
'parse_mode'=>'html',
]);
}
}
bot('editmessagetext',[
'chat_id'=>$chat_id,
'message_id'=>$mid + 1,
'text'=>"✅ <b>Yuborildi:</b> $x

❌ <b>Yuborilmadi:</b> $y",
'parse_mode'=>'html',
]);
}
}

if($text == "🤖 Bot holati"){
	if(in_array($cid,$admin)){
	if($holat == "Yoqilgan"){
		$xolat = "O'chirish";
	}
	if($holat == "O'chirilgan"){
		$xolat = "Yoqish";
	}
	bot('SendMessage',[
	'chat_id'=>$cid,
	'text'=>"<b>Hozirgi holat:</b> $holat",
	'parse_mode'=>'html',
	'reply_markup'=>json_encode([
	'inline_keyboard'=>[
[['text'=>"$xolat",'callback_data'=>"bot"]],
[['text'=>"Orqaga",'callback_data'=>"boshqarish"]]
]
])
]);
exit();
}
}

if($data == "xolat"){
	if($holat == "Yoqilgan"){
		$xolat = "O'chirish";
	}
	if($holat == "O'chirilgan"){
		$xolat = "Yoqish";
	}
	bot('deleteMessage',[
	'chat_id'=>$cid2,
	'message_id'=>$mid2,
	]);
	bot('SendMessage',[
	'chat_id'=>$cid2,
	'text'=>"<b>Hozirgi holat:</b> $holat",
	'parse_mode'=>'html',
	'reply_markup'=>json_encode([
	'inline_keyboard'=>[
[['text'=>"$xolat",'callback_data'=>"bot"]],
[['text'=>"Orqaga",'callback_data'=>"boshqarish"]]
]
])
]);
exit();
}

if($data == "bot"){
if($holat == "Yoqilgan"){
file_put_contents("holat.txt","O'chirilgan");
     bot('editMessageText',[
        'chat_id'=>$cid2,
       'message_id'=>$mid2,
       'text'=>"<b>Muvaffaqiyatli o'zgartirildi!</b>",
'parse_mode'=>'html',
'reply_markup'=>json_encode([
'inline_keyboard'=>[
[['text'=>"◀️ Orqaga",'callback_data'=>"xolat"]],
]
])
]);
}else{
file_put_contents("holat.txt","Yoqilgan");
     bot('editMessageText',[
        'chat_id'=>$cid2,
       'message_id'=>$mid2,
       'text'=>"<b>Muvaffaqiyatli o'zgartirildi!</b>",
'parse_mode'=>'html',
'reply_markup'=>json_encode([
'inline_keyboard'=>[
[['text'=>"◀️ Orqaga",'callback_data'=>"xolat"]],
]
])
]);
}
}

//📤 Kino Yuklash

if($text == "📤 Kino Yuklash"){
	bot('SendMessage',[
	'chat_id'=>$cid,
	'text'=>"Kino nomini kiriting: ",
	'parse_mode'=>'html',
	'reply_markup'=>$back,
]);
file_put_contents("step/$cid.step",'kinoo');
}

if($step == "kinoo"){
if(isset($text)){
	bot('SendMessage',[
	'chat_id'=>$cid,
	'text'=>"<b>$text Qabul Qilindi!</b>

Qaysi davlatda ishlab chiqarilgan.",
'parse_mode'=>'html',
'reply_markup'=>$back,
  ]);
  file_put_contents("step/test1.txt",$text);
  file_put_contents("step/$cid.step",'davlat');
}
}

if($step == "davlat"){
		if(in_array($cid,$admin)){
if(isset($text)){
	bot('SendMessage',[
	'chat_id'=>$cid,
	'text'=>"<b>$text Qabul Qilindi!</b>

Formatini kiriting: ",
'parse_mode'=>'html',
'reply_markup'=>$back,
  ]);
  file_put_contents("step/test2.txt",$text);
  file_put_contents("step/$cid.step",'formati');
}}
}

if($step == "formati"){
		if(in_array($cid,$admin)){
if(isset($text)){
	bot('SendMessage',[
	'chat_id'=>$cid,
	'text'=>"<b>$text Qabul Qilindi!</b>

janrini kiriting: ",
'parse_mode'=>'html',
'reply_markup'=>$back,
  ]);
  file_put_contents("step/test3.txt",$text);
  file_put_contents("step/$cid.step",'janri');
}}
}

if($step == "janri"){
		if(in_array($cid,$admin)){
if(isset($text)){
	bot('SendMessage',[
	'chat_id'=>$cid,
	'text'=>"<b>$text Qabul Qilindi!</b>

Ishlab chiqarilgan yili kiriting: ",
'parse_mode'=>'html',
'reply_markup'=>$back,
  ]);
  file_put_contents("step/test4.txt",$text);
  file_put_contents("step/$cid.step",'yili');
}}
}
if($step == "yili"){
		if(in_array($cid,$admin)){
if(isset($text)){
	bot('SendMessage',[
	'chat_id'=>$cid,
	'text'=>"<b>$text Qabul Qilindi!</b>

Kinoni tilini kiriting: ",
'parse_mode'=>'html',
'reply_markup'=>$back,
  ]);
  file_put_contents("step/test5.txt",$text);
  file_put_contents("step/$cid.step",'tili');

}}
}

if($step == "tili"){
		if(in_array($cid,$admin)){
if(isset($text)){
	bot('SendMessage',[
	'chat_id'=>$cid,
	'text'=>"<b>$text Qabul Qilindi!</b>

Kino haqida qisqa ma'lumot kiriting: ",
'parse_mode'=>'html',
'reply_markup'=>$back,
  ]);
  file_put_contents("step/test6.txt",$text);
  file_put_contents("step/$cid.step",'about');
}}
}

if($step == "about"){
		if(in_array($cid,$admin)){
if(isset($text)){
	bot('SendMessage',[
	'chat_id'=>$cid,
	'text'=>"<b>$text Qabul Qilindi!</b>

Kino avatar uchun rasm yuklang: ",
'parse_mode'=>'html',
'reply_markup'=>$back,
  ]);
  file_put_contents("step/test7.txt",$text);
  file_put_contents("step/$cid.step",'rasm');
}}
}

if($step == "rasm"){
	$rasm = $message->photo[0]->file_id;
		if(in_array($cid,$admin)){
	bot('SendMessage',[
	'chat_id'=>$cid,
	'text'=>"<b>Rasm Qabul Qilindi!</b>

Kinoni yuklang: ",
'parse_mode'=>'html',
'reply_markup'=>$back,
  ]);
  file_put_contents("step/test8.txt",$rasm);
  file_put_contents("step/$cid.step",'kino');
}
}



if($step=="kino"){
	$video = $message->video;
$file_id = $message->video->file_id;
$top=mysqli_query($connect,"SELECT * FROM kinolar ORDER BY kino_ids DESC LIMIT 1");
$a = mysqli_fetch_assoc($top);
$soni=$a['kino_ids'];
$s=$soni+1;
mysqli_query($connect, "INSERT INTO `kinolar`(`nomi`,`davlati`,`formati`,`janri`,`yili`,`tili`,`haqida`,`rasm_id`,`video_id`) VALUES ('$test1','$test2','$test3','$test4','$test5','$test6','$test7','$test8','$file_id')");
$res = mysqli_query($connect,"SELECT*FROM kinolar WHERE kino_ids = '$s'");
while($a = mysqli_fetch_assoc($res)){
$name = $a['nomi'];
$janri = $a['janri'];
$haqida = $a['haqida'];
$langs = $a['tili'];
$formats = $a['formati'];
$countrs = $a['davlati'];
$year = $a['yili'];
$rasmii = $a['rasm_id'];
}
bot('sendmessage',[
'chat_id'=>$shakh_akn,
'text'=>"Kino kanal va botga joylandi $kanalcha",
]);
bot('Sendphoto',[
'chat_id'=>$kanalcha,
'photo'=>$rasmii,
'caption'=>"<b>🎬 Nomi: $name

🧨 $haqida

🌎 Davlati: $countrs 
💽 Formati: $formats
🇺🇿 Tili: $langs
#⃣ Janri: $janri
🗓 Yili: $year

🟥 Kino kodi: <code>$s</code></b>",
'parse_mode'=>'html',
  'reply_markup'=>json_encode([
    'inline_keyboard'=>[
      [['text'=>"🎥 Kinoni yuklab olish",'url'=>"https://t.me/$bot?start=$s"],],
      [['text'=>"🖇️ Filmni ulashish",'url'=>"https://t.me/share/url?url=https://t.me/$bot?start=$s"]],
      ]
    ])
  ]);
unlink("step/$cid.step");
   unlink("step/test1.txt");
   unlink("step/test2.txt");
   unlink("step/test3.txt");
   unlink("step/test4.txt");
   unlink("step/test5.txt");
   unlink("step/test6.txt");
   unlink("step/test7.txt");
   unlink("step/test8.txt");
}

if(mb_stripos($text,"/start")!==false){
$exp=explode(" ",$text);
$link=$exp[1];
$resul= mysqli_query($connect,"SELECT * FROM kinolar WHERE kino_ids = '$link'");
$a = mysqli_fetch_assoc($resul);
$file= $a['video_id'];
$name=$a['nomi'];
 bot('SendVideo',[
   'video'=>$file,
   'chat_id'=>$cid,
   'caption'=>"$name

$reklama",
'reply_markup'=>json_encode([
'inline_keyboard'=>[
[['text'=>"❤️ Yoqtirish",'callback_data'=>"like=$link"]],
[['text'=>"🖇️ Filmni ulashish",'url'=>"https://t.me/share/url?url=https://t.me/$bot?start=$link"]],
]
])
   ]);
}
?>
