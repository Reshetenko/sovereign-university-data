## FIRMA DE ADAPTADOR

Método criptográfico que permite combinar una firma real con una firma adicional (llamada "firma de adaptador") para revelar un dato secreto. Este método funciona de tal manera que el conocimiento de dos elementos entre la firma válida, la firma de adaptador y el secreto permite deducir el tercero faltante. Una de las propiedades interesantes de este método es que si conocemos la firma de adaptador de nuestro par y el punto específico en la curva elíptica vinculado al secreto utilizado para calcular esta firma de adaptador, podemos entonces derivar nuestra propia firma de adaptador que coincidirá con el mismo secreto, y esto, sin haber accedido directamente al secreto en sí. En un intercambio entre dos partes que no se confían, esta técnica permite un desvelamiento simultáneo de dos informaciones sensibles entre los participantes. Este proceso elimina la necesidad de confianza durante transacciones instantáneas tales como un Coin Swap o un Atomic Swap. Tomemos un ejemplo para entenderlo mejor. Alice y Bob desean enviarse 1 BTC cada uno, pero no se confían. Por lo tanto, van a utilizar firmas de adaptador para anular la necesidad de confianza hacia la otra parte en este intercambio (por lo tanto, es un intercambio "atómico"). Proceden de la siguiente manera:
* Alice inicia este intercambio atómico. Ella crea una transacción $m_A$ que envía 1 BTC a Bob. Ella crea una firma $s_A$ que permite validar esta transacción gracias a su clave privada $p_A$ ($P_A = p_A \cdot G$), y utilizando un nonce $n_A$ y un secreto $t$ ($N_A = n_A \cdot G$ y $T = t \cdot G$):
$$s_A = n_A + t + H(N_A + T \parallel P_A \parallel m_A) \cdot p_A$$
&nbsp;
* Alice calcula la firma de adaptador $s_A'$ a partir del secreto $t$ y su verdadera firma $s_A$:
$$s_A' = s_A - t$$
&nbsp;
* Alice envía a Bob su firma de adaptador $sA'$, su transacción no firmada $m_A$, el punto correspondiente al secreto $T$ y el punto correspondiente al nonce $N_A$. Llamamos a esta información un "adaptador". Notemos que con simplemente esta información, Bob no está en capacidad de recuperar el BTC de Alice.
* Sin embargo, Bob puede verificar que Alice no está tratando de engañarlo. Para hacerlo, verifica que la firma de adaptador de Alice $s_A'$ corresponde bien a la transacción prometida $m_A$. Si la siguiente ecuación es correcta, entonces está convencido de que la firma de adaptador de Alice es válida:
$$s_A' \cdot G = N_A + H(N_A + T \parallel P_A \parallel m_A) \cdot P_A$$
&nbsp;
* Esta verificación proporciona a Bob garantías por parte de Alice, de tal manera que puede continuar el proceso de intercambio atómico con tranquilidad. Entonces, él crea a su vez su propia transacción $m_B$ enviando 1 BTC a Alice y su propia firma adaptadora $s_B'$, que estará vinculada con el mismo secreto $t$ que solo Alice conoce por el momento (Bob no tiene conocimiento de este valor $t$, sino solo de su punto correspondiente $T$ que Alice le ha proporcionado): $$s_B' = n_B + H(N_B + T \parallel P_B \parallel m_B) \cdot p_B$$
&nbsp;
* Bob envía a Alice su firma adaptadora $s_B'$, su transacción no firmada $m_B$, el punto correspondiente al secreto $T$ y el punto correspondiente al nonce $N_B$. Alice ahora puede combinar la firma adaptadora de Bob $s_B'$ con el secreto $t$, del cual solo ella tiene conocimiento, para calcular una firma válida $s_B$ para la transacción $m_B$ que le envía el BTC de Bob: 
$$s_B = s_B' + t$$
&nbsp;
$$(s_B' + t) \cdot G = N_B + T + H(N_B + T \parallel P_B \parallel m_B) \cdot P_B$$
&nbsp;
* Alice difunde esta transacción $m_B$ firmada en la blockchain de Bitcoin para recuperar el BTC que Bob le prometió. Bob se entera de esta transacción en la blockchain. Por lo tanto, está en capacidad de extraer la firma $s_B = s_B' + t$. Con esta información, Bob puede aislar el famoso secreto $t$ que necesitaba:
$$t = (s_B' + t) - s_B' = s_B - s_B'$$
&nbsp;
* Sin embargo, este secreto $t$ era la única información que faltaba a Bob para producir la firma válida $s_A$, a partir de la firma adaptadora de Alice $s_A'$, que le permitirá validar la transacción $m_A$ que envía un BTC desde Alice hacia Bob. Entonces, él calcula $s_A$ y difunde a su vez la transacción $m_A$: $$s_A = s_A' + t$$
&nbsp;
$$(s_A' + t) \cdot G = N_A + T + H(N_A + T \parallel P_A \parallel m_A) \cdot P_A$$
&nbsp;