# Subscriptions

The [Data API](../data_api.md) exposed by [Context Broker](../context_broker.md) implements *subscriptions* to configure notifications when cerain cnditions are met.

Subscriptions may share some fields and behavior with registrations (e.g., `id`, `entities`, `attributes`, `duration`, `url`, etc.), but are used for different purposes.

Example of a subscription:

    POST /v2/subscriptions
    Content-Type: application/json
    Fiware-service: smartown
    Fiware-servicepath: /roads

    {
      "subject": {
        "entities": [
          {
            "idPattern": ".*",
            "type": "Car"
          }
        ],
        "condition": {
            "attrs": [ "speed" ]
        }
      },
      "notification": {
        "http": {
            "url": "http://example.com/receiver"
        }
      }
    }


- Are used to configure notifications to be triggered when some conditions occur. See 
  [this document](how_notifications_work.md) for an introduction on this functionality.
- The URL associated to a subscription identifies a notification receiver, to which notifications covered
  by the subscription will be sent.
- They involve an unidirectional communication from Context Broker to the receiver. In other words,
  the receiver doesn't send any information back to the Context Broker (beyond the result of the notification
  delivery itself at HTTP level).
- Subscription management is part of the 
  [NGSIv2 specification](https://github.com/telefonicaid/fiware-orion/blob/master/doc/manuals/orion-api.md).