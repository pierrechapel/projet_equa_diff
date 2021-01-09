8) Si $H(x(t)) = H_0$ alors la schéma d'Euler va donner la même solution:  
   en effet, en notant $x_i'$ les points donnés par la méthode d'Euler appliquée aux équations modifiées, et $x_i$ les points donnés par les équations originales, on a clairement $x_0 =x_0'$ et $x_1= x_1'$ , donc $H(t_1)=H_0$. Comme $x_{i+1}'$ ne dépend que de $x_i'$ et de $H(t_i)$ on montre aisément par récurrence que 
     
    $\forall i \in \mathbb{N}, H(t_i) = H_0$ et $x_i'=x_i$, c'est à dire que les deux systèmes donnent les mêmes points.
   
9)  $$
    \frac{d}{dt} (H(x(t))-H_0) = (\delta -\frac{\gamma}{x_1}) \dot x_1 + (\beta - \frac{\alpha}{x_2}) \dot x_2
$$
en utilisant les équations modifiées du système, et puisque la partie correspodant aux équations de Lotka-Volterra se simplifie, on obtient:
$$
\frac{d}{dt} (H(x(t))-H_0) = - (H(x(t))-H_0) [(\delta -\frac{\gamma}{x_1})u_1(x) + (\beta - \frac{\alpha}{x_2}) u_2(x) ]
$$

On remarque que 
$$
\nabla H(x) = \begin{pmatrix}
 \delta -\frac{\gamma}{x_1}\\
 \beta - \frac{\alpha}{x_2}\\ 
\end{pmatrix}
$$

Ainsi, si on prend $u(x) = k \nabla H(x)$ , on obtient bien que   
$$
\frac{d}{dt} (H(x(t))-H_0) = -k ||\nabla H(x(t))||^2 (H(x(t))-H_0)
$$
Puisque 
$$ ||\nabla H(x(t))||^2 = (\delta -\frac{\gamma}{x_1})^2 + (\beta - \frac{\alpha}{x_2})^2 
$$
Comme $||x - \bar x|| \ge c > 0$ , alors $k||\nabla H(x(t))||^2$ est minorée par une constante $c'>0$, ce qui assure bien que $H(x(t))$ converge exponentiellement vers $H_0$ lorsque $t \rightarrow +\infty$ et $||x - \bar x|| \ge c >0$.  

  
10) Pour assurer la stabilité de $H$, il suffit donc d'implémenter les équations modifiées en prenant $u(x) = k \nabla H(x)$. Le rôle de $k$ est d'amplifier l'erreur entre la valeur de $H$ au point précédent et la valeur initiale $H_0$ pour que la correction à l'étape suivante soit plus drastique. Si k est pris trop grand, on risque de perdre la stabilité de $H$ qui peut se mettre à osciller entre des valeurs très positives et très négatives. En revanche, si il est choisi trop petit, les corrections seront trop lentes pour être intéressantes.  
On peut vérifier ce raisonnement en calculant $H(x^{j+1})-H(x_0)$ en fonction de $H(x^{j})-H(x_0)$ et de k au premier ordre:
$$
H(x^{j+1})-H(x_0) = [ H(x^{j})-H(x_0) ] - k||\nabla H(x^j)||^2 (H(x^{j})-H(x_0)) dt + O(dt^2)
$$
donc
$$
H(x^{j+1})-H(x_0) = [ H(x^{j})-H(x_0) ][1 - k||\nabla H(x^j)||^2 (H(x^{j})-H(x_0)) dt ] + O(dt^2)
$$
On voit bien que si $k$ est trop grand, les corrections seront trop grandes, et $H(x(t))$ oscillera avec des grandes amplitudes autour de $H_0$. 