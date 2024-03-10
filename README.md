### Este es un codigo basico para hacer movimiento con un cubo con las teclas WASD 
Es algo muy basico y eficad si quieres crear un juego que Player sea un cubo.

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Mover : MonoBehaviour
{
    private Rigidbody _rb;
    [SerializeField] private float moveSpeed = 1f;
    [SerializeField] private float maxSpeed = 10f; // Establece la velocidad máxima deseada

    void Start()
    {
        _rb = GetComponent<Rigidbody>();
    }

    void Update()
    {
        MovePlayer();
    }

    void MovePlayer()
    {
        float xValue = Input.GetAxis("Horizontal") * moveSpeed;
        float zValue = Input.GetAxis("Vertical") * moveSpeed;

        Vector3 movement = new Vector3(xValue, 0f, zValue);

        _rb.AddForce(movement, ForceMode.Acceleration);

        // Limita la velocidad para evitar atravesar objetos a velocidades extremas
        _rb.velocity = Vector3.ClampMagnitude(_rb.velocity, maxSpeed);
    }

    private void OnCollisionEnter(Collision collision)
    {
        // Detiene el movimiento si la colisión ocurre en la dirección opuesta al movimiento actual del jugador
        if (Vector3.Dot(_rb.velocity.normalized, collision.contacts[0].normal) < -0.5f)
        {
             _rb.velocity = Vector3.zero;
             _rb.angularVelocity = Vector3.zero;
        }
    }
}
```
