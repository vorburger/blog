# How to log to Google Cloud Logging as JSON from Java with SLF4j

Add <https://github.com/logfellow/logstash-logback-encoder> and put this into your `logback.xml`:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
    <!-- Use JSON format for scalable logging suitable for Google Cloud Logging -->
    <appender name="STDOUT" class="ch.qos.logback.core.ConsoleAppender">
        <encoder class="net.logstash.logback.encoder.LogstashEncoder">
            <!-- logstash-logback-encoder writes timestamps in the default TimeZone of the JVM, but GCP wants UTC -->
            <timeZone>UTC</timeZone>

            <!-- Align field names with Google Cloud Structured Logging requirements;
                 see https://docs.cloud.google.com/logging/docs/structured-logging,
                 and https://docs.cloud.google.com/logging/docs/reference/v2/rest/v2/LogEntry. -->
            <fieldNames>
                <!-- GCP expects 'timestamp', logstash-logback-encoder defaults to '@timestamp' -->
                <timestamp>timestamp</timestamp>

                <!-- GCP expects 'severity', logstash-logback-encoder defaults to 'level' -->
                <level>severity</level>

                <!-- Ignore levelValue as severity is sufficient for GCP -->
                <levelValue>[ignore]</levelValue>

                <!-- Disable logstash-logback-encoder's '@version' field as GCP doesn't use it -->
                <version>[ignore]</version>

                <!-- GCP expects 'message' which is the default for logstash-logback-encoder -->
            </fieldNames>
        </encoder>
    </appender>

    <!-- Wrap STDOUT in AsyncDisruptorAppender for better performance, decoupling logging from I/O -->
    <appender name="ASYNC_STDOUT" class="net.logstash.logback.appender.LoggingEventAsyncDisruptorAppender">
        <appender-ref ref="STDOUT" />
    </appender>

    <!-- Suppress verbose internal logging from certain libraries if needed -->
    <!-- <logger name="org.apache" level="WARN" /> -->

    <root level="INFO">
        <appender-ref ref="ASYNC_STDOUT" />
    </root>
</configuration>
```

Alternatives:
* https://github.com/hkupty/penna
* https://github.com/avaje/avaje-simple-logger
* https://github.com/savoirtech/slf4j-json-logger
