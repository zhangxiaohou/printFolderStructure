将此代码放在根目录下，即可生成该文件目录结构表
<pre><code>
<?php
function scanFile($dir){
    if(strstr($dir,".") || !is_dir($dir)){
      //含有“.”的文件基本是不需要的，所以没有输出，可根据实际情况修改或删除
        return $dir;
    }else{
        $file1 = scandir($dir);
        foreach($file1 as $key => $value){
            $ans [$value] = scanFile ($dir."/".$value);
        }
        return $ans;
    }
}
function printFile($file,$level){
    foreach($file as $key => $value){
      //  print_r($key."<br>");  printFile($value,$level + 1);
        if(is_array($value)){
           // print_r($key);
            for($i = 0;$i < $level;$i++){
                   echo "|&nbsp;&nbsp;&nbsp;";
            }
            echo "|--".$key."<br>";
            printFile($value,$level + 1);
        }
    }
}
$dir = dirname(__FILE__);
$file = scanFile($dir);
foreach($file as $key => $value){
   // print_r($value);
}
 printFile($file,0);
?>
</code></pre>
