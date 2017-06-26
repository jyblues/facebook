### 사용자 토큰으로 유저 정보 검증하는 방법입니다.

```
define('facebook_app_id', '****************');
define('facebook_app_secret_code', '****************');

function GetFacebookAccessToken($client_access_token)
{
	// 
	$url = 'https://graph.facebook.com/oauth/access_token';
	$postData = 'client_id='.facebook_app_id.'&client_secret='.facebook_app_secret_code.'&grant_type=client_credentials';

	echo $url.'<br/>';
	echo $postData.'<br/>';

	$curl = curl_init();
	curl_setopt($curl, CURLOPT_URL, $url);
	curl_setopt($curl, CURLOPT_FAILONERROR, 1);
	curl_setopt($curl, CURLOPT_RETURNTRANSFER, 1);
	curl_setopt($curl, CURLOPT_FOLLOWLOCATION, 1);
	curl_setopt($curl, CURLOPT_POST, true);
	curl_setopt($curl, CURLOPT_POSTFIELDS, $postData);

	$response = curl_exec($curl);
	if($response === false)
		return false;

	var_dump($response); echo '<br/>';

	$response_array = json_decode($response, true);

	$access_token_response = $response_array['access_token'];

	$url = 'https://graph.facebook.com/debug_token?input_token='.$client_access_token.'&access_token='.$access_token_response;
	echo $url.'<br/>';

	$curl2 = curl_init();
	curl_setopt($curl2, CURLOPT_URL, $url);
	curl_setopt($curl2, CURLOPT_FAILONERROR, 1);
	curl_setopt($curl2, CURLOPT_RETURNTRANSFER, 1);
	curl_setopt($curl2, CURLOPT_FOLLOWLOCATION, 1);

	$response = curl_exec($curl2);
	if($response === false)
		return false;

	var_dump($response);

	$response_array = json_decode($response, true);

	return $response_array;
}

```
