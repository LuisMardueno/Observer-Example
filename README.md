
# Observer-Example
Ejemplo práctico de observer en C#

El uso del patrón de observer nos permite crear una lista de suscriptores y notificarlos cuando el publicante actualice su estatus sin necesidad de enviar la notificación a todos los clientes que no necesiten actualmente esa información.

Por ejemplo, usando este código [Observer Example](https://dotnetfiddle.net/oWIMQm):

Supongamos que, en un juego donde el jugador cuenta con una cantidad de dinero para comprar edificios, estos modifican su valor de acuerdo a la cantidad de edificios que hay en la partida. Para notificar a los demás jugadores de una manera eficiente, se crea una lista de observadores interesados en conocer el precio de los edificios. Una vez un jugador compra uno de estos, el precio se modifica y es notificado a los jugadores.

```csharp
public void BuyAmount(int n, Player player)
{
    int total = this.CalculatePrice(n);
    if (player.SpendMoney(total))
    {
        this.amount += n;

        // Para cada observador se le notifica el cambio de la cantidad
        foreach (Observer observer in amountObservers)
        {
            observer.OnNotify(this.amount);
        }
    }
}


